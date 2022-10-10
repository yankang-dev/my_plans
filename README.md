https://blog.csdn.net/weixin_43664418/article/details/103482005
https://blog.csdn.net/Butterfly_resting/article/details/89639414
https://blog.csdn.net/jackfrued/article/details/44921941
https://blog.csdn.net/Butterfly_resting/article/details/89668661
file:///C:/Users/ywx477562/Downloads/%E9%9D%A2%E8%AF%95%E5%90%88%E9%9B%86/pdf/%E5%90%8E%E7%AB%AF-Java%E5%A4%9A%E7%BA%BF%E7%A8%8B.pdf
https://blog.csdn.net/weixin_43664418/article/details/102644728
https://blog.csdn.net/weixin_44337261/article/details/98477048?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.essearch_pc_relevant&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.essearch_pc_relevant
https://www.cnblogs.com/crazymakercircle/p/14365487.html
给定 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

说明：你不能倾斜容器，且 n 的值至少为 2。



图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。

 

示例:

输入: [1,8,6,2,5,4,8,3,7]
输出: 49
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function(height) {
    // 双指针 
    let s =   0
    let q = height.length -1
    let area = (q-s) * Math.min(height[q],height[s])
    while(s != q) {
        if (height[s] < height[q]) {
            s++
        } else {
            q--
        }
        area = Math.max(area, (q-s) * Math.min(height[q],height[s]))
    }
    return area
};

————————————————
版权声明：本文为CSDN博主「baoleilei6」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_34629352/article/details/103845214
