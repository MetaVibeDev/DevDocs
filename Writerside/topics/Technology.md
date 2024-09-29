# 硬核技术知识点集合
1. react-native原生的Animated可以结合传入的position计算页面的偏移量实现动画效果
    组件传入position 检测页面的位置  使用position.interpolate可以换算成百分比，比如根据页面偏移量实现顶部导航栏的滑块跟随页面移动
   这里的outputRange是偏移的范围

            
            const translateX = position.interpolate({
            inputRange,
            outputRange: inputRange.map(
            i => (i - index) * (textWidths[index] + 24),
            ),
            });

    
    



2. 学习到了一种很高级的方法可以更加简洁明了 采用键值对的方法 如果遇到多重switch 或者if 可以选择这样写 
![formatDate.png](formatDate.png)


