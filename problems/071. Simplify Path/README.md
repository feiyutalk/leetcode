# 071. Simplify Path

# Description

Given an absolute path for a file (Unix-style), simplify it.

For example,
**path** = `"/home/"`, => `"/home"`
**path** = `"/a/./b/../../c/"`, => `"/c"`

# Solution

昨天刚好看到一个博客，讲的是面向对象和面向过程，以及数据结构和算法，作者画了个四象图，感觉挺好的，这里通过表格的形式展示一下

|      |   数据结构    |  算法   |
| ---- | :-------: | :---: |
| 面向过程 | 线性表，队列，栈等 | 冒泡 排序 |
| 面向对象 | 类，对象，容器类  | 构造，析构 |

这样分，其实上也不是特别的合理，因为，面向过程和面向对象都有其解决问题的优点以及局限。面向对象的思想在问题空间和对象之间建立映射，通过在对象空间中建模来求解问题空间。面向过程则是将问题转化成一些逻辑推到，从问题的开始推导到问题的结束。

数据结构是静态的，算法是动态的，这里面，算法是真正解决问题的东西，但是很多算法都依赖于好的数据结构，所以，要把算法学扎实，还是需要把经典的数据结构掌握好。好了，扯得有点多，这道题目就是典型的借助栈这种数据结构来求解的问题，为什么呢?或者我们是怎么发现需要用栈来求解的呢？

首先栈这种特点在于后进先出，这就和回溯算法的性质特别的吻合，后面被调用的函数先返回，也与括号匹配相吻合，后面出现的括号要先被匹配掉。递归回溯也好，括号匹配也好，虽然场景看上去不同，但是问题的本质是一样的，就是具有**后进先出**的特点，所以，但凡有我们抓住问题的主要矛盾是后进先出，我们就可以考虑用栈这种数据结构。

路径中的..，实际上就是将目录回退一格，那被回退的目录是哪一个呢？是后面进来的那个目录，这种场景也是符合后进先出的。

```java
class Solution {
    public String simplifyPath(String path) {
        //boundary condition
        if(path == null || path.length() == 0)
            return "";
        if(path.length() == 1)
            return path;
        //normal condition
        String[] dirs = path.split("/");
        Stack<String> stack = new Stack<>();
        for(String dir : dirs){
            if(dir.equals("..")){
                if(!stack.isEmpty())
                    stack.pop();
            }else if(!dir.equals(".") && !dir.isEmpty()){
                stack.push(dir);
            }
        }
        if(stack.isEmpty())
            return "/";
        
        String result = "";
        while(!stack.isEmpty()){
            result = "/" + stack.pop() + result;
        }
        return result;
    }
}
```

