<template>
    <div class="w-swiper-wrap"
         @touchstart="touchStart($event)"
         @touchend="touchEnd($event, swiperEl)"
         @touchmove="touchMove($event)"
         @mouseover="touceHover(true)"
         @mouseout="touceHover(false, swiperEl)">
	    <slot></slot>
	    <ul class="w-paging-list" v-if="wSwiperOptions.pageShow">
		    <li v-for="(val, index) in pagingArr" :class="{'w-active': index == pageIndex}" @click="pagingClick(index, swiperEl)"></li>
	    </ul>
    </div>
</template>

<script>
  export default {
  	props: ['wSwiperOptions'],
    name: '',
    data() {
      return {
        swiperEl: '',
	      intervalId: '',
	      currentIndex: 0,
	      pagingArr: [],
	      pageIndex: 0,
	      startX: 0,
	      moveMar: 0
      }
    },
    components: {},
    mounted() {
    	this.init();
    },
    methods: {
    	init(){
		    this.swiperEl = document.getElementById('wSwiperWrap');
		    let el = this.swiperEl;
		    let elChild = this.swiperEl.children;
		    for(let i = 0;i < elChild.length;i++){
			    this.pagingArr.push({
				    class: ''
			    });
		    };
		    //复制首尾节点并添加
		    let first = elChild[0].cloneNode(true);
		    let last = elChild[elChild.length - 1].cloneNode(true);
		    el.insertBefore(last, elChild[0]);
		    el.appendChild(first);
		    //初始化位置第一个
		    el.style.transform = `translate3d(-${el.offsetWidth}px, 0px, 0px)`;
		    //轮播初始化
		    this.autoPlay(el);
		    //绑定左右切换按钮
		    this.bindNextPrevClick(el);
	    },
	    autoPlay(el){
    		if(!this.wSwiperOptions.autoPlay){
			    return
		    }
		    this.intervalId = setInterval(() => {
			    this.judgeCurrent(el);
			    this.currentIndex++;
			    this.moveAnimate(el);
			    this.pagingParallelism(el);
		    }, this.wSwiperOptions.time);
	    },
	    judgeCurrent(el){
		    if(this.currentIndex == el.children.length - 2){
			    this.currentIndex = 0;
			    el.style.transform = `translate3d(-${el.offsetWidth}px, 0px, 0px)`;
			    el.style.transition = '0s';
		    }else if(this.currentIndex == -1){
			    this.currentIndex = el.children.length - 3;
			    el.style.transform = `translate3d(-${el.offsetWidth * (this.currentIndex + 1)}px, 0px, 0px)`;
			    el.style.transition = '0s';
		    };
	    },
	    bindNextPrevClick(el){
		    this.addEnent('w-next-slide-btn', 'click', () => {
		    	this.nextPrevPlay(el, 1);
		    });
		    this.addEnent('w-prev-slide-btn', 'click', () => {
			    this.nextPrevPlay(el, -1);
		    });
	    },
	    nextPrevPlay(el, type){
		    clearInterval(this.intervalId);
		    this.judgeCurrent(el);
		    this.currentIndex += type;
		    this.moveAnimate(el);
		    this.autoPlay(el);
		    this.pagingParallelism(el);
	    },
	    pagingParallelism(el){
    		let len = el.children.length;
		    if(this.currentIndex == -1 || this.currentIndex == len - 3){
			    this.pageIndex = len - 3;
		    }else if(this.currentIndex == len - 2){
			    this.pageIndex = 0;
		    }else{
			    this.pageIndex = this.currentIndex;
		    }
	    },
	    pagingClick(index, el){
		    clearInterval(this.intervalId);
		    this.currentIndex = index;
		    this.moveAnimate(el);
		    this.autoPlay(el);
		    this.pagingParallelism(el);
	    },
	    touchStart(e){
		    clearInterval(this.intervalId);
		    this.startX = e.targetTouches[0].pageX;
	    },
	    touchMove(e){
		    this.moveMar = e.targetTouches[0].pageX - this.startX;
	    },
	    touchEnd(e, el){
		    if(this.moveMar > (10)){
			    this.nextPrevPlay(el, -1);
		    }else if(this.moveMar < -10){
			    this.nextPrevPlay(el, 1);
		    }
		    this.moveMar = 0;
	    },
	    touceHover(bool, el){
		    if(!this.wSwiperOptions.hoverPause){
			    return
		    }
		    clearInterval(this.intervalId);
		    if(!bool){
			    this.autoPlay(el);
		    };
	    },
    	moveAnimate(el){
		    let startX =  -this.currentIndex * el.offsetWidth;
		    let endX = startX - el.offsetWidth;
		    el.style.transform = `translate3d(${endX}px, 0px, 0px)`;
		    el.style.transition = `${this.wSwiperOptions.speed}s`;
	    },
	    addEnent(el, type, callback){
    	  document.getElementsByClassName(el)[0].addEventListener(type, callback)
	    }
    }
  }
</script>

<style scope>
	ul{
		margin: 0;
		padding: 0;
		list-style: none;
	}
  .w-swiper-wrap{
	  position: relative;
	  overflow: hidden;
    width: 100%;
	  height: 100%;
	  cursor: default;
  }
  #wSwiperWrap{
	  position: absolute;
	  display: flex;
	  width: 100%;
	  height: 100%;
  }
  .w-swiper-wrap .w-prev-slide-btn{
	  display: flex;
	  align-items: center;
	  justify-content: center;
		position: absolute;
		top: 50%;
	  left: 20px;
	  min-width: 2em;
	  min-height: 2em;
		transform: translateY(-50%);
	  border-radius: 50%;
		background: #fff;
	}
  .w-swiper-wrap .w-next-slide-btn{
	  display: flex;
	  align-items: center;
	  justify-content: center;
	  position: absolute;
	  top: 50%;
	  right: 20px;
	  min-width: 2em;
	  min-height: 2em;
	  transform: translateY(-50%);
	  border-radius: 50%;
	  background: #fff;
  }
  .w-slide{
	  flex-shrink: 0;
	  width: 100%;
	  height: 100%;
  }
	.w-paging-list{
		display: flex;
		justify-content: center;
		position: absolute;
		bottom: 6%;
		width: 100%;
	}
	.w-paging-list li{
		width: .6em;
		height: .6em;
		margin: 0 .5em;
		border-radius: 50%;
		background: #fff;
	}
	.w-paging-list li.w-active{
		background: #147ffa;
	}
</style>
