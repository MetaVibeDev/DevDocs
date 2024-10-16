# 硬核技术知识点集合

###### 1. react-native原生的Animated可以结合传入的position计算页面的偏移量实现动画效果

   组件传入position 检测页面的位置  使用position.interpolate可以换算成百分比，比如根据页面偏移量实现顶部导航栏的滑块跟随页面移动
   这里的outputRange是偏移的范围
    <code-block lang="javascript">
    const translateX = position.interpolate({
        inputRange,
        outputRange: inputRange.map(
        i => (i - index) * (textWidths[index] + 24),
        ),
    });
    </code-block>

###### 2. 一种很高级的方法可以更加简洁明了 采用键值对的方法 如果遇到多重switch 或者if 可以选择这样写 

![formatDate.png](formatDate.png)

###### 3. CSS样式管理的知识深化：全局字体样式的系统化管理

*    在实际开发中，经常会遇到界面风格不一致的问题，尤其是多个开发者或在不同模块工作时，容易形成不同的样式导致"风格漂移"。UI规范虽然可以作为指导，但开发过程中仍然存在随意定义字体样式的现象，导致后续维护困难。
*    知识 ：本次通过“字体样式统一定义”的方式，深入地解决了这个问题。
   学会了一种面向全局响应UI规范的样式定义方式，能够使得样式更具一致性并易于维护。
   拆解UI方案并进行标准化，确保所有组件都遵循同一套规则，实现了全局的样式化管理。提升在维护大型应用时的代码复用率，减少了未来重复调整的机会。

###### 4. i18n的结构化组织
*    之前由于没有详细了解i18n的写法所以将所有的都写在同一个文件的同一级下面，导致维护的时候会非常麻烦，添加的时候只能在底部加，后期行数多的话会比较冗余
  * 知识：将每个页面的翻译内容做一个父级，这个页面的翻译内容都放在这个父级下面，也相当于模块化，后期添加和维护起来，结构更加清晰

###### 5. 超轻量级状态管理库jotai（优点：超轻量！！！）
[https://www.npmjs.com/package/jotai](https://www.npmjs.com/package/jotai)
* 安装：
<code-block>
 yarn add jotai
</code-block>
* 使用（方法1）：
<code-block lang="javascript">
import { atom, useAtom } from 'jotai';
const isVerifyCodeWrongTipOpenAtom = atom(false);//注册

const [verifyCode, setVerifyCode] = useAtom(verifyCodeAtom);//像useState一样使用
</code-block>
* 使用（方法2）：
<code-block lang="javascript">
//use-isVerifyCodeWrongTipOpen.ts
import { atom, useAtom } from "jotai";
const isVerifyCodeWrongTipOpenAtom = atom(false);
export const UseIsVerifyCodeWrongTipOpen = () => {
  return useAtom(isVerifyCodeWrongTipOpenAtom);
};

//page.tsx
import {UseIsVerifyCodeWrongTipOpen} from './use-isVerifyCodeWrongTipOpen'
const [isVerifyCodeWrongTipOpen, setIsVerifyCodeWrongTipOpen] = UseIsVerifyCodeWrongTipOpen();
setIsVerifyCodeWrongTipOpen(false)
</code-block>


