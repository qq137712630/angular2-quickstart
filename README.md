#angular2-quickstart


[CMD下，目录树生成：tree /f >list.txt](http://jingyan.baidu.com/article/5d368d1e0add873f60c057f6.html)	

[TOCM]

[TOC]


#00

 - [5 MIN QUICKSTART](https://angular.io/docs/ts/latest/quickstart.html)

#01

 - [THE HERO EDITOR](https://angular.io/docs/ts/latest/tutorial/toh-pt1.html)

#02-2016年1月16日21:29:02

 - [MASTER/DETAIL](https://angular.io/docs/ts/latest/tutorial/toh-pt2.html)

#03-2016年1月18日10:52:52

 - [MULTIPLE COMPONENTS](https://angular.io/docs/ts/latest/tutorial/toh-pt3.html)
	
		We refactor the master/detail view into separate components	
		我们重构了主/详细信息视图成独立的组件

Our app is growing. Use cases are flowing in for reusing components, passing data to components, and creating more reusable assets. Let's separate the heroes list from the hero details and make the details component reusable.

我们的应用程序越来越大。用例都流淌在重复使用的组件，将数据传递到组件，并创造更多的可重用资产。让我们分开英雄细节的英雄榜，使细节部分可重复使用。

##Where We Left Off 我们离开的地方

Before we continue with our Tour of Heroes, let’s verify we have the following structure. If not, we’ll need to go back and follow the previous chapters.

在我们继续我们的巡回赛的英雄，让我们来验证，我们有以下的结构。如果不是这样，我们需要回去，并按照前面的章节。

	angular2-tour-of-heroes
	│  index.html
	│  package.json
	│  tsconfig.json
	│  
	├─app
	│      app.component.ts
	│      boot.ts
	│      
	└─node_modules

###Keep the app transpiling and running 保持应用程序transpiling运行

We want to start the TypeScript compiler, have it watch for changes, and start our server. We'll do this by typing

我们要启动TypeScript，有它监视的更改，然后开始我们的服务器。我们将通过键入做到这一点

	npm start

This will keep the application running while we continue to build the Tour of Heroes.

这将继续运行的应用程序，同时，我们继续打造英雄之旅。

##Making a Hero Detail Component 制作一个英雄详图构件

Our heroes list and our hero details are in the same component in the same file. They're small now but each could grow. We are sure to receive new requirements for one and not the other. Yet every change puts both components at risk and doubles the testing burden without benefit. If we had to reuse the hero details elsewhere in our app, the heroes list would tag along for the ride.

我们的英雄列表和我们的英雄的细节都在在同一文件中同样的部件。他们是小，但现在每一个可能增长。我们一定要接受新的要求之一，而不是其他。然而，每一个变化的风险使这两个组件和双打无裨益的测试负担。如果我们必须在我们的应用程序在其他地方重复使用英雄细节，英雄榜将标记凑凑热闹。

Our current component violates the [Single Responsibility Principle](https://blog.8thlight.com/uncle-bob/2014/05/08/SingleReponsibilityPrinciple.html). It's only a tutorial but we can still do things right — especially if doing them right is easy and we learn how to build Angular apps in the process.

我们目前的组件违反了单一职责原则。这只是一个教程，但我们还是可以做正确的事情 - 特别是如果这样做他们的权利是很简单的，我们学习如何在这个过程中建立角的应用程序。

Let’s break the hero details out into its own component.

让我们打破了英雄的细节伸到自己的分量。

### Separating the Hero Detail Component 分离英雄详图构件

Add a new file named hero-detail.component.ts to the app folder and create HeroDetailComponent as follows.

添加一个新的文件，命名为英雄detail.component.ts到应用程序文件夹并创建HeroDetailComponent如下。

	hero-detail.component.ts (initial version)

	import {Component} from 'angular2/core';
	@Component({
	  selector: 'my-hero-detail',
	})
	export class HeroDetailComponent {
	}

	Naming conventions
	命名约定

	We like to identify at a glance which classes are components and which files contain components.
	我们喜欢快速识别哪些类成分，哪些文件包含的组件。
	
	Notice that we have an AppComponent in a file named app.component.ts and our new HeroDetailComponent is in a file named hero-detail.component.ts.
	请注意，我们有一个文件名为app.component.ts的AppComponent我们的新HeroDetailComponent是在一个名为hero-detail.component.ts。	

	All of our component names end in "Component". All of our component file names end in ".component".
	在“Component”我们所有的组件名称结尾。在“.component”我们所有的组件文件名结尾。
	
	We spell our file names in lower dash case (AKA "kebab case") so we don't worry about case sensitivity on the server or in source control.
	我们拼出我们的文件名中下划线的情况下（又名"kebab case"），所以我们不担心在服务器上还是在源代码控制区分大小写。

We begin by importing the `Component` function from Angular so that we have it handy when we create the metadata for our component.

我们首先从角导入 `Component` 功能，使我们有它方便当我们创建的元数据，我们的组件。

We create metadata with the @Component decorator where we specify the selector name that identifies this component's element. Then we export the class to make it available to other components.

我们创建了@Component装饰，我们指定标识此组件的元素选择名称的元数据。然后，我们出口类使其向其他组件可用。

When we finish here, we'll import it into AppComponent and refer to its <my-hero-detail> element.

当我们在这里完成，我们将其导入到AppComponent并参考其<my-hero-detail>元素。

### Hero Detail Template-英雄详细信息模板

At the moment, the Heroes and Hero Detail views are combined in one template in AppComponent. Let’s cut the Hero Detail content from AppComponent and paste it into the new template property of HeroDetailComponent.

目前，英雄和英雄详细视图组合在AppComponent一个模板。让我们从切开的AppComponent英雄详细内容并将其粘贴到HeroDetailComponent的新模板属性。

We previously bound to the selectedHero.name property of the AppComponent. Our HeroDetailComponent will have a hero property, not a selectedHero property. So we replace selectedHero with hero everywhere in our new template. That's our only change. The result looks like this:

我们以前绑定到AppComponent的selectedHero.name财产。我们HeroDetailComponent都会有一个英雄属性，而不是selectedHero财产。因此，我们在我们的新模板的英雄代替selectedHero无处不在。这是我们唯一的变化。结果如下：
	
	hero-detail.component.ts (template)

	template: `
	  <div *ngIf="hero">
	    <h2>{{hero.name}} details!</h2>
	    <div><label>id: </label>{{hero.id}}</div>
	    <div>
	      <label>name: </label>
	      <input [(ngModel)]="hero.name" placeholder="name"/>
	    </div>
	  </div>
	`,

Now our hero detail layout exists only in the HeroDetailComponent.

现在只存在于HeroDetailComponent我们的英雄详细布局。

### Add the hero property 加入英雄属性

Let’s add that hero property we were talking about to the component class.

让我们补充说，英雄属性，我们都在谈论的组件类。

	public hero: Hero;

Uh oh. We declared the hero property as type Hero but our Hero interface is over in the app.component.ts file. We have two components, each in their own file, that need to reference the Hero interface.

嗯哦。我们申报的英雄属性类型的英雄，但我们的英雄界面是多年来在app.component.ts文件。我们有两部分组成，各自在自己的文件，这需要引用的英雄界面。

We solve the problem by relocating the Hero interface from app.component.ts to its own hero.ts file.

我们通过重新定位从app.component.ts英雄接口自身hero.ts文件解决问题。
	
	hero.ts (Exported Hero interface)

	export interface Hero {
	  id: number;
	  name: string;
	}

We export the Hero interface from hero.ts because we'll need to reference it in both component files. Add the following import statement near the top of both app.component.ts and hero-detail.component.ts.

我们从hero.ts出口英雄接口，因为我们需要引用它在这两个组件文件。添加下面的import语句到 app.component.ts 和 hero-detail.component.ts 的顶部。 hero-detail.component.ts 和app.component.ts（导入英雄接口）

	hero-detail.component.ts and app.component.ts (Import the Hero interface)
	
	import {Hero} from './hero';

### The hero property is an input 英雄属性是一个输入

The HeroDetailComponent must be told what hero to display. Who will tell it? The parent AppComponent!

该HeroDetailComponent必须被告知英雄来显示。谁将会告诉它？父AppComponent！

The AppComponent knows which hero to show: the hero that the user selected from the list. The user's selection is in its selectedHero property.

该AppComponent知道要显示的英雄：用户从列表中选择的英雄。用户的选择是在其selectedHero属性。

We will soon update the AppComponent template so that it binds its selectedHero property to the hero property of our HeroDetailComponent. The binding might look like this:

我们将很快更新AppComponent模板，以便它的selectedHero属性绑定到我们HeroDetailComponent的英雄属性。结合可能是这样的：

	<my-hero-detail [hero]="selectedHero"></my-hero-detail>

Notice that the hero property is the target of a property binding — it's in square brackets to the left of the (=).

请注意，英雄属性是一个属性绑定的目标 - 它在方括号的（=）的左侧。

Angular insists that we declare a target property to be an input property. If we don't, Angular rejects the binding and throws an error.

Angular坚持认为，我们宣布一个目标属性为输入性。如果我们不这样做，角拒绝结合并引发错误。

We explain input properties in more detail here where we also explain why target properties require this special treament and source properties do not.

我们更详细地解释了输入性在这里，我们也解释了为什么目标属性需要这种特殊的黄泥和源属性没有。

There are a couple of ways we can declare that hero is an input. We'll do it by adding an inputs array to the @Component metadata.

有几种方法，我们可以宣布，主人公是一个输入。我们将通过增加一个输入数组的@Component元数据做到这一点。

	inputs: ['hero']

Learn about the @Input() decorator way in the Attribute Directives chapter.

了解有关属性指令章@input（）装饰方法。

## Refresh the AppComponent 刷新AppComponent

We return to the AppComponent and teach it to use the HeroDetailComponent.

我们回到AppComponent并教它使用HeroDetailComponent。

We begin by importing the HeroDetailComponent so we can refer to it.

我们首先导入HeroDetailComponent，所以我们可以参考它。

	import {HeroDetailComponent} from './hero-detail.component';

Find the location in the template where we removed the Hero Detail content and add an element tag that represents the HeroDetailComponent.

找到我们删除了英雄详细内容模板中的位置，然后添加一个表示HeroDetailComponent的元素标签。

	<my-hero-detail></my-hero-detail>

	my-hero-detail is the name we set as the selector in the HeroDetailComponent metadata.
	我的英雄细节是，我们设定为在HeroDetailComponent元数据选择器的名称。

The AppComponent’s template should now look like this
该AppComponent的模板现在应该是这样的

	app.component.ts (Template)

	template:`
	  <h1>{{title}}</h1>
	  <h2>My Heroes</h2>
	  <ul class="heroes">
	    <li *ngFor="#hero of heroes"
	      [class.selected]="hero === selectedHero"
	      (click)="onSelect(hero)">
	      <span class="badge">{{hero.id}}</span> {{hero.name}}
	    </li>
	  </ul>
	  <my-hero-detail [hero]="selectedHero"></my-hero-detail>
	`,

Thanks to the binding, the HeroDetailComponent should receive the hero from the AppComponent and display that hero's detail beneath the list. The detail should update every time the user picks a new hero.
多亏了绑定，HeroDetailComponent应该从AppComponent收到的英雄，并显示列表下方的英雄的细节。细节应该更新用户选择一个新的英雄每次。

It's not happening yet!

它没有发生呢！

We click among the heroes. No details. We look for an error in the console of the browser development tools. No error.

我们的英雄中单击。没有详细说明。我们期待在的浏览器开发工具的控制台错误。没有错误。

It is as if Angular were ignoring the new tag. That's because it is ignoring the new tag.

这是因为如果Angular被忽视的新标签。这是因为它忽略了新的标签。

### The directives array

A browser ignores HTML tags and attributes that it doesn't recognize. So does Angular.

浏览器会忽略HTML标签和属性，它不承认。所以呢Angular。

We've imported HeroDetailComponent, we've used it in the template, but we haven't told Angular about it.

我们进口HeroDetailComponent，我们已经在模板中使用它，但我们还没有告诉Angular了。

We tell Angular about it by listing it in the metadata directives array. Let's add that array property to the bottom of the @Component configuration object, immediately after the template and styles properties.

我们告诉 Angular 它通过列出它的元数据指令阵列。让我们的数组属性添加到@Component配置对象的底部， `template` 和 `styles` 属性之后。

	directives: [HeroDetailComponent]

### It works! 有用！

When we view our app in the browser we see the list of heroes. When we select a hero we can see the selected hero’s details.

当我们查看浏览器我们的应用程序，我们看到英雄的名单。当我们选择一个英雄，我们可以看到所选英雄的详细信息。

What's fundamentally new is that we can use this HeroDetailComponent to show hero details anywhere in the app.

什么是全新的是，我们可以利用这个HeroDetailComponent在应用程序的任何地方显示出英雄的细节。

We’ve created our first reusable component!

我们已经创建了第一个可重用的组件！

### Reviewing the App Structure 回顾应用程序结构

Let’s verify that we have the following structure after all of our good refactoring in this chapter:
让我们来验证，我们有以下的结构毕竟我们在本章中良好的重构：
	
	│  index.html
	│  list.txt
	│  package.json
	│  README.md
	│  tsconfig.json
	│  
	├─app
	│      app.component.ts
	│      boot.ts
	│      hero-detail.component.ts
	│      hero.ts
	│      
	└─node_modules

Here are the code files we discussed in this chapter.
以下是我们在本章中所讨论的代码文件。

### The Road We’ve Travelled 路我们已经入住时间旅行

Let’s take stock of what we’ve built.
让我们来盘点一下，我们已经建立了库存。

 - We created a reusable component
 - 我们创建了一个可重用的组件
 - 
 - We learned how to make a component accept input
 - 我们学会了如何做一个组件接受输入
 - 
 - We learned to bind a parent component to a child component.
 - 我们学会了一个父组件绑定到一个子组件。
 - 
 - We learned to declare the application directives we need in a directives array.
 - 我们学会了声明，我们需要在一个指令阵列的应用程序的指令。

## The Road Ahead 前进的道路

Our Tour of Heroes has become more reusable with shared components.
我们的英雄之旅变得更加可重用与共享组件。

We're still getting our (mock) data within the AppComponent. That's not sustainable. We should refactor data access to a separate service and share it among the components that need data.
我们仍然得到AppComponent在我们​​的（模拟）数据。这是不可持续的。我们应该重构数据获得单独的服务和需要的数据的组件之间共享。

We’ll learn to create services in the next tutorial chapter.
我们将学习如何在一个教程章创建服务。