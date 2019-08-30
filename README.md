# apicloud_alert
APIClould 自定义弹出框


&emsp;&emsp;在大家的项目里应该会出现一些弹窗选择，你可能用了 confirm、prompt，也可能用了 dialogBox，使用这些模块总是不错的，但也许其样式满足不了你的需求。
在这我给大家分享一个简单的弹窗实现，主要利用 frame 实现。

&emsp;&emsp;先上个效果图：

&emsp;&emsp;点击遮照部位可以关闭弹窗。

&emsp;&emsp;这个实现起来非常简单，总共就两个步骤：
&emsp;&emsp;第一步：打开一个全屏的 frame，并设置半透明

    api.openFrame({
                    name: 'dialog',
                    url: './html/dialog.html',
                    rect: {
                            x:0,
                            y:0,
                            w:api.winWidth,
                            h:api.winHeight
                    },
                    bgColor: 'rgba(0,0,0,0.6)',
                            bounces: false
            });


&emsp;&emsp;第二步：在打开的 frame 里，设置一个白底的 div，里面可以自定义任何你想要的东西，比如 alert 的确定按钮什么的。
&emsp;&emsp;下面的 js 代码主要实现点击 div 外，将弹窗关闭的效果：

    $('#dialog').addClass('in');
            apiready = function(){
                    $(document.body).on('touchend',function(e){
                            var dialog = $("#dialog")[0];
                            if(!$.contains(dialog, e.target)){
                                    $('#dialog').removeClass('in');
                                    setTimeout(function(){
                                            api.closeFrame();
                                    },200);
                            }
                    });
            };

&emsp;&emsp;这里监听了 touchend 事件，然后判断了点击的区域是后在 div 内，不在就closeframe。各位看官可以根据自己需求，选择加不加监听，也可以控制遮照的透明度。
