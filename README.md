### 1. 页面基本结构
        1. loading  
        canvas.circle  
        text  
        2. home  
        title  
        subtitle  
        entitle  
        hand-wrap...  
        3. result  
        title  
        answer  avatar...  
### 2. canvas.getContext('2d') 返回一个用于在画布上绘图的环境
        beginPath()起始一条路径，或重置当前路径
        moveTo();把路径移动到画布中的指定点，不创建线条
        arc(x,y,半径,开始角度,结束角度,画的方向，顺时针or逆时针) 创建弧/曲线（用于创建圆形或部分圆）Math.PI , 圆周率 3.1415926。 例：ctx.arc(50,50,50,0+1.5*Math.PI,1.5*Math.PI+(2*Math.PI)*10/100,false);
        圆心点 （50,50）
        closePath()创建从当前点回到起始点的路径
        fillStyle属性设置或返回用于填充绘画的颜色、渐变或模式。
        fill()填充当前的路径
### 2. 导出图片地址
        导出图片 右键图目录git bash here，执行命令 ls > aaa.txt，打开aaa.txt  ctrl+h 将换行符选择放到第1个input，第2个input替换框放","css/，把首位没用的部分去掉，还有.css和.less文件删除
### 3. css3动画
        animation: name duration timing-function delay iteration-count direction;  
        动画名称 动画花费时间  动画速度曲线     动画开始之前的延时  动画播放次数   是否轮流反向播放动画  
        .shake-wrap{animation:shake-wrap 2s linear匀速 both infinite 循环播放transform-origin:40% 100%;}  
        none不改变默认行为。forwards当动画完成后，保持最后一个属性值（在最后一个关键帧中定义）。backwards在 animation-delay 所指定的一段时间内，在动画显示之前，应用开始属性值（在第一个关键帧中定义）。both向前和向后填充模式都被应用。  
        @keyframes animationname {keyframes-selector {css-styles;}}  
        定义动画的名称  动画时长的百分比 合法的值：0-100% from（与 0% 相同）to（与 100% 相同） ;一个或多个合法的 CSS 样式属性  
        @keyframes shake-wrap{0%{transform:rotate(0deg)}10%{transform:rotate(5deg)}20%{transform:rotate(-5deg)}30%{transform:rotate(5deg)}40%{transform:rotate(-5deg)}100%{transform:rotate(0deg)}}  
        transform: none|transform-functions;  
        rotate(angle)    定义 2D 旋转，在参数中规定角度。  
        transform:rotate(5deg);  
        transform-origin: 50% 50% 0 ;改变被转换元素的位置  
                              视图在x      y   z位置,默认值50% 50% 0  
        transform-origin:40% 100%;  
### 4. 摇一摇
        ondevicemotion重力感应  
        'ondevicemotion' in window  
        document.CustomEvent自定义事件  
        document.createEvent('Event');创建事件  
        event.initEvent;初始化创建的事件  
        document.dispatchEvent(aaa.event);初始化，dispatchEvent() 方法给节点分派一个合成事件,传入的参数是通过createEvent创建的事件  
        window.addEventListener('click',obj,false)第2个参数可传递对象  
        例如：var obj = {a:'bb',handleEvent:function(){alert(2)}} ;window.addEventListener('click', obj, false);
### 5. velocity动画
        http://www.mrfront.com/docs/velocity.js/option.html  
        complete：动画完成后执行的操作  
        duration：执行时间，执行了多久，动画过程耗费的时间，精确到毫秒$('div').velocity('callout.flash',{duration:1})  
        stop：停止动画$('div').velocity('stop');  
        transition.expandOut，缩小到消失  
        transition.expandIn，放大到全部显示  
        $('.result-avatar').velocity('transition.expandIn',{display:'block'});  
        $('.result-text').velocity('transition.bounceIn',{display:'block'})   X  
        $('.result-text').velocity('transition.bounceIn');  
        7个结果的展示-1  
            完成一个结果的情况  
                $('.result-avatar-wrap').velocity({rotateY:'3600deg'},{duration:3000,complete:function(){  
                        $('.result-avatar-default').velocity('transition.expandOut',{complete:function(){  
                                $('.result-avatar').velocity('transition.expandIn',{display:'block',complete:function(){  
                                    $('.result-text').velocity('transition.bounceIn');  
                                }});  
                        }});  
                }});  
            完成七个结果的随机情况  
                var random = parseInt(Math.random()*7),.2332432  
                    $t = $('.result ul li').eq(random);  
                $t.show().siblings().hide();//兄弟节点  
                $('.result-avatar-wrap').velocity({rotateY:'3600deg'},{duration:3000,complete:function(){  
                //$t.find('.result-avatar-wrap')  
                        $('.result-avatar-default',$t).velocity('transition.expandOut',{complete:function(){  
                                $('.result-avatar',$t).velocity('transition.expandIn',{display:'block',complete:function(){  
                                    $('.result-text',$t).velocity('transition.bounceIn');  
                                }});  
                        }});  
                }});  
            去重  
                var random = parseInt(Math.random()*count),  
                $t = $('.result ul li:not(.noshow)').eq(random)  //clash是result下面的ul li，但是不包括 li的class是noshow  
            //<div class="result"><ul><li class="noshow"></li><li></li></ul></div>;  
                count--;  
                if(count<=0){  
                    count = 7;  
                    $('.result ul li').removeClass('noshow');  
                }  
                $t.show().addClass('noshow').siblings().hide();  
                $('.result-avatar-wrap',$t).velocity({rotateY:'3600deg'},{duration:3000,complete:function(){  
                        $('.result-avatar-default',$t).velocity('transition.expandOut',{complete:function(){  
                                $('.result-avatar',$t).velocity('transition.expandIn',{display:'block',complete:function(){  
                                    $('.result-text',$t).velocity('transition.bounceIn');  
                                }});  
                        }});  
                }});  
### 6. 手晃动动画
        .an_shake{-webkit-animation:shake_s 1s ease-in-out infinite;animation:shake_s 1s ease-in-out infinite;-webkit-transform-origin:50% 50%;transform-origin:50% 50%;}  
        @keyframes shake_s{  
            0%{-webkit-transform:rotate(0);transform:rotate(0);}  
            10%{-webkit-transform:rotate(-20deg);transform:rotate(-20deg);}  
            20%{-webkit-transform:rotate(0deg);transform:rotate(0deg);}  
            30%{-webkit-transform:rotate(-20deg);transform:rotate(-20deg);}  
            40%{-webkit-transform:rotate(0deg);transform:rotate(0deg);}  
            100%{-webkit-transform:rotate(-20deg);transform:rotate(-20deg);}  
        }  
### 7. 分享
        页面部分
            <div class="share">  
                <div class="mask"></div>  
                <div class="share-text"></div>  
            </div>  
        .share{display: none;position: absolute;left: 0;top: 0;width: 100%;height: 100%;z-index: 2;}  
        .mask{position: absolute;left: 0;top: 0;width: 100%;height: 100%;background-color: rgba(0,0,0,0.8);}  
        .share-text{position: absolute;right: 10px;top: 10px;background: url(../css/share.png) no-repeat center/cover;width: 125px;height: 110px;}  
        绑定  
                    $('.result').on('click','.result-btn',function(){  
                        $('.share').show();  
                    });  
                    $('body').on('click','.share',function(){  
                        $('.share').hide();  
                    });  






