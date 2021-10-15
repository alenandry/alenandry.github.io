# angular-组件传值

# 子组件获取父组件数据和方法

<!-- 这是一个链接 [Markdown 语法](https://alenandry.github.io "最好的markdown教程")。 -->

```js
<!-- 子组件 form -->
<app-form [shows]="shows" [run]="run" [news]="this">form 组件</app-form>
```

\*\*

```
<!-- 父组件中定义 run 方法 -->
run(){
    alert('父组件方法')
 }
```

在父组件中挂载子组件,通过绑定属性的方法绑定传递给子组件的数据(属性,方法,包括父组件本身)\
run 是传递给子组件的方法,注意不要加()

\*\*

```
import { Component, OnInit,Input } from '@angular/core';
```

在子组件中引入 Input 模块

\*\*

```
export class FormComponent implements OnInit {

  @Input() shows:boolean
  @Input() run:any
  @Input() news:this

  constructor() { }
  ngOnInit(): void {
  }

  getrun(){
    this.run()
    alert(this.news.title)
  }
}
```

在子组件类中通过 @Input 装饰器接收父组件传递过来的数据(属性,方法,包括父组件本身)

\*\*

```
<button (click)="getrun()">执行父组件方法</button>
```

子组件中定义方法执行父组件传递过来的方法

# 父组件获取子组件数据和方法

\*\*

```
<app-form #formId>form 组件</app-form>
public msg = '子组件的一个msg'
```

在子组件挂载处定义个名称或者 id,且定义一个获取数据和执行方法的事件

\*\*

```
@ViewChild('formId') form: any
```

通过@ViewChild 接受子组件传递过来的数据和方法

\*\*

```
父组件中定义个方法
<button (click)="getchildMsg()">获取form子组件的msg</button>
<button (click)="getchildRun()">执行form子组件的方法</button>
 getchildMsg() {
    alert(this.form.msg)
  }
 getchildRun(){
    this.form.formrun()
  }
```

执行父组件中的事件就可以获得子组件的数据和方法

# 通过 Output 和 EventEmitter

\*\*

```
import { Component, OnInit, Output, EventEmitter } from '@angular/core';
```

子组件中引入 Output 和 EventEmitter

\*\*

```
<button (click)="setrun()">通过@Output执行父组件数据</button>

@Output() private out = new EventEmitter()

setrun(){
    alert(this.out.emit('子组件的数据'))
}
```

子组件中定义方法,通过@Output()声明一个变量\
子组件中实例化 EventEmitter\
子组件中 setrun 是要执行的方法

\*\*

```
<app-form (out)="run($event)">form 组件</app-form>
run(e) {
  console.log(e)
  alert('父组件方法')
}
```

父组件中定义一个方法接收,父组件中的 run 方法接收的就是子组件的方法执行时传递给父组件的数据
