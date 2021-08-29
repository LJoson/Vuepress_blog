---
title: 概览
sidebar: true
date: 2020-03-21
sidebarDepth: 0
isShowComments: true
---

<div style="height: 120px">
	<Boxx :changeTime='changeTime' />
</div>

<p style='display: block;
          margin-bottom: 8px;'>
	<img id='imgShow' :class='active' :src='imgSrc'/>
</p>


<div id='category'>

[【分类】](/categories/)

</div>

<div id='tag'>

[【标签】](/tag/)

</div>

<div id='fj'>

[【电子设计类】](/views/ee/star.html) | [【AI及大数据类】](/views/AI/2020baidustar.html)| [【计算机技术类】](/views/cs/GlimmerOS.html) 

</div>

<div id='se'>

 [【游戏设计类】](/views/game/16.html) | [【笔记类】](/views/notes/git.html)|[【杂谈】](/views/freetalk/wsl.html)|[【算法类】](/views/algorithm/otsu.html)

</div>

<CatalogGraph  root='/views/' title='概览' :height='320' />



<style lang='stylus' scoped> 
	@keyframes rowup {
        0% {
            -webkit-transform: translate3d(0, 15%, 0);
            transform: translate3d(0, 15%, 0);
        }
        100% {
            -webkit-transform: translate3d(0, -100%, 0);
            transform: translate3d(0, -100%, 0);
        }
    }
    .list{
        border: 1px solid #999;
        /*margin: 20px auto;*/
        position: relative;
        height: 200px;
        overflow: hidden;
        text-align: center;
        font-size: 14px;
        border-radius: 3px;
        width: 150px;
    }
    .list .rowup{
        -webkit-animation: 50s rowup linear infinite normal;
        animation: 50s rowup linear infinite normal;
        position: relative;
    }

	img.noActive{
		opacity: 0;
		transition: opacity 5s linear;
		pointer-events: none;
	}
	img.active{
		opacity: 1;
		transition: opacity 5s linear;
		pointer-events: none;
	} 
	.content__default:not(.custom) img {
	    max-width: 20% !important;
	    margin-top: -10px;
	    //padding-left: 26%;
	}

	#category {
		width:100px;
		height:100px;
		float: right;
		border-radius: 25%;
		background:#ffff0059;
		transition:width 2s, height 2s;
		-moz-transition:width 2s, height 2s, -moz-transform 2s; /* Firefox 4 */
		-webkit-transition:width 2s, height 2s, -webkit-transform 2s; /* Safari and Chrome */
		-o-transition:width 2s, height 2s, -o-transform 2s; /* Opera */
	}
	#category:hover {
		width:100px;
		height:100px;
		transform:rotate(360deg);
		-moz-transform:rotate(360deg); /* Firefox 4 */
		-webkit-transform:rotate(360deg); /* Safari and Chrome */
		-o-transform:rotate(360deg	); /* Opera */
	}
	
	#tag {
		width:100px;
		height:100px;
		float: right;
		border-radius: 25%;
		background:#ffff0059;
		transition:width 2s, height 2s;
		-moz-transition:width 2s, height 2s, -moz-transform 2s; /* Firefox 4 */
		-webkit-transition:width 2s, height 2s, -webkit-transform 2s; /* Safari and Chrome */
		-o-transition:width 2s, height 2s, -o-transform 2s; /* Opera */
	}
	#tag:hover {
		width:100px;
		height:100px;
		transform:rotate(360deg);
		-moz-transform:rotate(360deg); /* Firefox 4 */
		-webkit-transform:rotate(360deg); /* Safari and Chrome */
		-o-transform:rotate(360deg	); /* Opera */
	}
	
	#category p,#tag p {
	    margin: 0;
	    line-height: 100px;
	    text-align: center;
	    font-size: 15px;
	}
	#category,#tag {
        margin-top: 18px;
    }
	
	#fj,#se {
		margin-top: 27px;
	}
	
	@media screen and (max-width: 960px){
	    .catalog-graph {
	        display: none;
	    }
		.content__default:not(.custom) img {
		    max-width: 35% !important;
		    margin: 17px;
		    padding-left: 26%;
		}
		.list {
		    margin: auto;
		}
		#fj {
			font-size: 13px !important;
			margin-top: 28px;
		}
		#se {
			font-size: 13px !important;
		}
		#category,#tag {
		    margin: 3% 0;
		    margin-top: 28px;
			width:80px;
			height:80px;
		}
		#category:hover,#tag:hover {
			width:80px;
			height:80px;
		}
		#category p,#tag p {
		    line-height: 80px;
	        font-size: 14px;
	    }
	}
	
	@media screen and (max-width: 320px){
		#fj,#se {
			font-size: 10px !important;
		}
	}
</style>


