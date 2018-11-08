# 使用less的when循环生成css（grid组件）
> 之前在vue中使用sass写过grid，还抱怨为什么大家喜欢用sass这个需要ruby环境的玩意儿，现在项目用的less，发现深坑处处，列举如下
## 先上代码
- less写法
```less

.grid-stack-item(@count) when(@count>0){
  .grid-stack-item((@count - 1));
  .grid-stack-item[data-gs-width='@{count}']{
    width: percentage(@count/24)
  }
  .grid-stack-item[data-gs-x='@{count}'] {
		left: percentage(@count/24)
	}
  .grid-stack-item[data-gs-min-width='@{count}'] {
    min-width: percentage(@count/24)
  }
  .grid-stack-item[data-gs-max-width='@{count}'] {
    max-width: percentage(@count/24)
  }

}
.grid-stack{
  .grid-stack-item(24)
}
```
- 生成结果
```less
.grid-stack {
	>.grid-stack-item[data-gs-width='1'] {
		width: 8.3333333333%;
	}
	>.grid-stack-item[data-gs-width='2'] {
		width: 16.6666666667%;
	}
	>.grid-stack-item[data-gs-width='3'] {
		width: 25%;
	}
	>.grid-stack-item[data-gs-width='4'] {
		width: 33.3333333333%;
	}
	>.grid-stack-item[data-gs-width='5'] {
		width: 41.6666666667%;
	}
	>.grid-stack-item[data-gs-width='6'] {
		width: 50%;
	}
	>.grid-stack-item[data-gs-width='7'] {
		width: 58.3333333333%;
	}
	>.grid-stack-item[data-gs-width='8'] {
		width: 66.6666666667%;
	}
	>.grid-stack-item[data-gs-width='9'] {
		width: 75%;
	}
	>.grid-stack-item[data-gs-width='10'] {
		width: 83.3333333333%;
	}
	>.grid-stack-item[data-gs-width='11'] {
		width: 91.6666666667%;
	}
	>.grid-stack-item[data-gs-width='12'] {
		width: 100%;
	}
}
```


## 要点
- 使用when实现loop
less里没有while，用when，在这里声明class（？？？从css那边论是class，从less这边论，说function不太对，说class又不是css那个class）；
class支持参数与when关键字
- 变量运算
less支持变量运算，但是用减法时需要注意与连接符区分，@变量-1应写成 @变量 - 1；
- class名的变量引用
在class名中引用变量生成多个class名是loop的重点，但是写成.class-name-@变量会报错，应写为.class-name-@{变量名}，如果是属性选择器，需要指定字符串的，直接在{}外加上引号即可
