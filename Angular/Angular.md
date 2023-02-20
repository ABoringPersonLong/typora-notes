# 1. 框架背景

Angular 是一个由 Google 维护的开源 JavaScript 框架，用于在 HTML 和 JavaScript 中构建 Web 应用程序，是三大框架之首。

不管是 1 还是 2，Angular 最显著的特征就是其**整合性**。涵盖了 M、V、C/VM 等各个层面，不需要组合、评估其它技术就能完成大部分前端开发任务。这样可以有效降低决策成本，提高决策速度，对需要快速起步的团队是非常有帮助的。

由于它是从一个用来做原型的框架演化而来的，加上诞生时间很早（2009 年，作为对比，jQuery 诞生于 2006 年），当时生态不完善，连模块化机制都得自己实现。

但 Angular2 就不同了，发布于 2016 年 9 月份，它是基于 ES6 来开发的，它的起点更高，整合了现代前端的各种先进理念，在框架、文档工具等各个层面提供了全方位的支持。

在 Angular 中最具特色的就是**依赖注入**系统了，它把后端开发中用来解决复杂问题、实现高弹性设计的技术引入了前端。

# 2. Angular CLI

## 1. 安装

Angular CLI 用于简单，快速构建 Angular2 项目，只要掌握几行命令就能扣减前端架构。依赖于 Node.js 和 npm。

```sh
# 安装脚手架
npm install -g @angular/cli

# 创建项目
ng new 项目名称

# 启动项目，--open 表示打开浏览器
ng serve --open
```

## 2. 目录结构

- **src/app/app.component.html**：当前 app 组件的模板文件
- **src/app/app.component.scss**：当前 app 组件的样式文件
- **src/app/app.component.spec.ts**：当前 app 组件的测试文件
- **src/app/app.component.ts**：当前 app 组件的 js/ts 文件
- **src/app/app.module.ts**：所有组件的入口文件
- **src/app/app-routing.module.ts**：当前项目的路由配置文件

## 3. 架构

### 1. 模块

模块组件的特征在于可以用于执行单个任务的代码块。您可以从代码（类）中导出值。Angular 应用程序被称为模块，并使用许多模块构建您的应用程序。Angular 的基本构建块是可以从模块导出的**组件**类。

```js
export class AppComponent {
  title = '01-demo' // 定义变量，在 html 中可以以 {{ title }} 的形式调用
}
```

### 2. 组件

组件是拥有模板的控制器类，主要处理页面上的应用程序和逻辑的视图。组件可以拥有独立的样式。

注册组件，使用 @Component 注释，可以将应用程序拆分为更小的部分。

#### 1. 创建组件

在项目根目录下使用 ng 命令 `ng generate component 组件名称` 创建的组件会自动生成在 `app.module.ts` 中的引用，推荐使用 ng 命令生成组件：

```sh
ng generate component 组件名称
# 简写
ng g c 组件名称
```

```js
@Component({
  selector: 'app-root', // 选择器，将来渲染到 app-root 标签中
  templateUrl: './app.component.html', // 组件模板文件的 url
  styleUrls: ['./app.component.scss'] // 组件样式文件的 url
})
```

@Component 最常用的几个选项：

- **selector**：这个 css 选择器用于在模板中标记出该命令，并触发该指令的实例化
- **templateUrl**：组件模板文件的 url
- **styleUrls**：组件样式文件的 url
- **template**：组件的内联模板
- **styles**：组件内联样式

### 3. 模板

#### 1. 插值表达式

跟 vue 一样

#### 2. 属性绑定

1. Attribute 绑定

   ```html
   <div [id]="'box'">111</div>
   ```

2. 类绑定

   ```html
   <!-- 单一类绑定 -->
   <div [class.box]="true">222</div>
   <!-- 多重类绑定 -->
   <div [class]="'box1 box2 box3'">333</div>
   <div [class]="{ box1: true, box2: true, box3: false }">444</div>
   <div [class]="['box1', 'box2', 'box3']">555</div>
   ```

3. 样式绑定

   ```html
   <!-- 单一样式绑定 -->
   <div [style.font-size]="'50px'">666</div>
   <!-- 带单位的单一样式绑定 -->
   <div [style.font-size.px]="'50'">777</div>
   <!-- 多重样式绑定 -->
   <div [style]="'background-color: red; color: #fff'">888</div>
   <div [style]="{ backgroundColor: 'red', color: '#fff' }">999</div>
   ```

4. 条件判断

   `*ngIf` 是直接影响元素是否被渲染，而非控制元素的显示和影藏

   ```jsx
   <!-- if -->
   <div *ngIf="true">max content</div>
   <div *ngIf="false">min content</div>
   <!-- *ngIf 内部解析完后，是这样的 -->
   <ng-template [ngIf]="true">
     <div>template content</div>
   </ng-template>
   <!-- if else 语法，ng-container 和 ng-template 都不会解析为标签 -->
   <ng-container *ngIf="true; else templateRef">
     <div>条件为 true</div>
   </ng-container>
   <ng-template #templateRef>
     <div>条件为 false</div>
   </ng-template>
   <!-- switch -->
   <div [ngSwitch]="type">
     <div *ngSwitchCase="1">
       type: 1
     </div>
     <div *ngSwitchCase="2">
       type: 2
     </div>
     <div *ngSwitchDefault>
       type != 1 && type != 2
     </div>
   </div>
   
   export class HelloComponent {
     type = 1
   }
   ```

5. 循环语句

   解析器会把 `let item`、`let index`、`let even` 和 `let odd` 翻译成命名变量 `color`、`index`、`even` 和 `odd`

   微语法解析器接收 of，会将它的首字母大写（Of），然后加上属性的指令名（ngFor）前缀，它最终生成的名字是 ngFor 的输入属性（colors）`NgFor` 指令在列表上循环，每个循环中都会设置和重置它自己的上下文对象上的属性。这些属性包括 `index`、`even` 和 `odd` 以及一个特殊的属性名 `$implicit`（隐式变量）

   Angular 将 `let-item` 设置为此上下文中 `$implicit` 属性的值，它是由 `NgFor` 用当前迭代中的 `colors` 初始化的

   ```jsx
   <div *ngFor="let item of colors let index = index let even = even let odd = odd">
     {{ item }} == {{ index }} == {{ even }} == {{ odd }}
   </div>
   <!-- *ngFor 内部解析完后，是这样的 -->
   <ng-template ngFor let-item [ngForOf]="colors" let-index="index" let-even="even" let-odd="odd">
     <div>{{ item }} == {{ index }} == {{ even }} == {{ odd }}</div>
   </ng-template>
   
   export class HelloComponent {
     colors = ['red', 'blue', 'yellow', 'green']
   }
   ```

6. 事件绑定

   Angular 的事件绑定语法由等号左侧括号内的目标事件名和右侧引号内的模板语句组成。目标事件名是 `click`，模板语句是 `onSave()`

   事件对象通过 `$event` 传递

   ```jsx
   <input type="text" (input)="onInput($event)">
   <button (click)="onSave($event)">保存</button>
   
   export class HelloComponent {
     onInput(event: Event) {
       console.log('输入框输入了', event)
     }
     onSave(event: MouseEvent) {
       console.log('点击了按钮', event)
     }
   }
   ```

7. 双向绑定

   双向绑定是应用中的组件共享数据的一种方式。使用双向绑定来个侦听事件并在父组件和子组件之间同步更新值 `ngModel` 指令只对表单元素有效，所以在使用之前需要导入 `FormsModule` 板块

   app.module.ts 文件：

   ```typescript
   import { FormsModule } from '@angular/forms'
   
   @NgModule({
     imports: [
       FormsModule
     ]
   })
   ```

   使用：

   ```jsx
   输入：<input type="text" [(ngModel)]="username"><br>
   你输入了：{{ username }}
   
   export class HelloComponent {
     username = ''
   }
   ```

8. 模板引用变量（vue 中的 ref）

   模板变量可以帮助你在模板的另一部分使用这个部分的数量。使用模板变量，你可以执行某些任务，比如响应用户输入或微调应用的表单在模板中，需使用井号 `#` 来声明一个模板变量。下列模板变量 `#username` 语法在 `<input>` 元素上声明了一个名为 `username` 的变量

   ```jsx
   <input #input type="text">
   <button (click)="getInputValue(input.value)">获取输入的值</button>
   
   export class HelloComponent {
     getInputValue(value: string) {
       console.log(value)
     }
   }
   ```

9. 表单控件

   使用表单控件有三个步骤。

   1. 在你的应用中注册响应式表单模块，该模块声明了一些你要用在响应式表单中的指令。
   2. 生成一个新的 `FormControl` 实例，并把它保存在组件中。
   3. 在模板中注册这个 `FormControl`。

   **注册响应式表单模块**

   要使用响应式表单控件，就要从 `@angular/forms` 包中导入 `ReactiveFormsModule`，并把它添加到你的 NgModule 的 `imports` 数组中。

   app.module.ts 文件：

   ```typescript
   import { ReactiveFormsModule } from '@angular/forms'
   
   @NgModule({
     imports: [
       ReactiveFormsModule
     ]
   })
   ```

   要注册一个表单控件，就要导入 `FormControl` 类并创建一个 `FormControl` 的新实例，将其保存为类的属性。

   ```jsx
   name：<input type="text" [formControl]="name">
   <button (click)="setName()">将name改为zhangsan</button>
   <br>
   name.value：{{ name.value }}
   
   import { FormControl } from '@angular/forms'
   
   export class HelloComponent {
     name = new FormControl('')
   
     setName() {
       // 修改 name 值可以通过 FormControl 提供的 setValue() 方法
       this.name.setValue('zhangsan')
     }
   }
   ```

10. 表单控件分组

    表单中通常会包含几个相互关联的控件。响应式表单提供了两种把多个相关控件分组到同一个输入表单中的方法。

    要将表单组添加到此组件中，请执行以下步骤。

    1. 创建一个`FormGroup`实例。
    2. 把这个`FormGroup`模型关联到视图。
    3. 保存表单数据。

    **创建一个 FormGroup 实例**

    在组件类中创建一个名叫`loginForm` 的属性，并设置为`FormGroup`的一个新实例。要初始化这个`FormGroup`，请为构造函数提供一个由控件组成的对象，对象中的每个名字都要和表单控件的名字一一对应：

    ```tsx
    <form [formGroup]="loginForm">
      username：<input type="text" formControlName="username">
      password：<input type="text" formControlName="password">
    </form>
    login.value.username：{{ loginForm.value.username }}<br>
    login.value.password：{{ loginForm.value.password }}
    
    import { FormControl, FormGroup } from '@angular/forms'
    
    export class HelloComponent {
      loginForm = new FormGroup({
        username: new FormControl('zhangsan'),
        password: new FormControl('123')
      })
    }
    ```

    