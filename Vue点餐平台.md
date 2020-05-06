1、vue全局组件

	语法
	Vue.component(tagName,options);
	tagName 组件名称
	options 配置项
		data 数据，是个函数
		template 模板，内容为html结构（必须参数）不仅仅只有这两个配置项（还有methods等），
示例
	<div id="app">
        <dean></dean>
    </div>

	<template id="btn">
        <div>
            <button @click=click>点击{{count}}次</button>
            <span>winnie</span>
        </div>
    </template>

	Vue.component("dean",{
            template:"#btn",
            data(){
                return{
                    count:0
                }
            },
            methods:{
                click(){
                    this.count++;
                }
            }
        })

2、Vue局部组件（尽量不要使用全局组件）

	语法
	new Vue({
		components:{
			tagName:options,
			tagName:options,
		}
	})
	局部组件用的是components，全局组件是component
示例
	
	new Vue({
            el:"#app", //el:的替代写法，$mount('') 如new Vue({}).$mount('#app')
            components:{
                deanWinnie:{     //第一个局部组件
                    template:"#nav",
                    data() {
                        return {
                            somebody:['dean','winnie','sam','mark']
                        }
                    },
                    methods: {
                        touch(){
                            alert("don't touch me")
                        }
                    },
                },
                winnieDean:{        //第二个局部组件
                    template:"#list",
                    data() {
                        return {
                            somebody:['Linda','Helen','Tom','Kevie']
                        }
                    },
                    methods: {
                        touch(){
                            alert("don't touch me")
                        }
                    }, 
                }
            }
        })

3.props 在组件上定义一些属性用来传递数据（传递给组件里的结构使用）
	
	语法
	组件里 props:['属性名','属性名'....]
	模板里 {{属性名}}
	标签里 <组件 属性名="值" 属性名="值"></组件>

示例
	
	<div id="app">
        <dean-winnie name="林清玄" book="《白雪少年》"></dean-winnie>
        <dean-winnie name="钱钟书" book="《围城》"></dean-winnie>
    </div>
    <template id="box">
        <div class="box-list">
            <p>{{name}}</p>
            <p>{{book}}</p>
        </div>
    </template>
	
	new Vue({
        el:"#app",
        components:{
            deanWinnie:{
                template:"#box",
                props:['name','book']
            }
        }
    })

4、solt 插槽，用于分发内容
	
	语法
	template里定义<slot></slot>
	组件标签对里使用（标签对里的标签能被解析）
	
	具名插槽 给slot添加name属性就叫具名插槽
	语法 
		template里定义<slot name="属性名"></slot>
		组件标签对里使用<p slot="属性名"></p>

示例
	
	<template id="demo">
	    <div>
	        <p>我的世界里</p>
	        <slot name="winnie"></slot>
	        <slot name="dean"></slot>
	    </div>
	</template>

	<div id="app">
	    <you>
	        <h1 slot="winnie">我是雯</h1>
	        <h2 slot="dean">我是涛</h2>
	    </you>
	</div>

5、父子组件  即组件里面再套一个一个组件

	示例
	<template id="bigBox">
       <div class="box">
           <p>this is box</p>
           <slot name="referral"></slot>
           <winnie>
                <h2 slot="book">《呐喊》</h2>
                <h2 slot="author">鲁迅</h2>
           </winnie>
           <winnie>
            <h2 slot="book">《围城》</h2>
            <h2 slot="author">钱钟书</h2>
        </winnie>
       </div>
	</template>
 
	<template id="smallBox">
       <div class="item">
           <h1>I CAN SEE IT</h1>
            <slot name="book"></slot>
            <slot name="author"></slot>
       </div>
	</template>
	

7、父子组件之间相互传递数据
	
	语法
	1、父组件向子组件传递数据（自动传）
		1、在子组件标签里通过v-bind绑定一条属性，属性的值为父组件的数据名称
		2、在子组件里利用props属性把已经绑定的属性名写进去
		3、在子组件的template里就可以使用了
	2、子组件向父组件传数据（主动传，事件触发）使用自定义事件
	
	自定义事件
		1、在发数据组件的methods里定义一个方法，方法内容如下
		this.$emit('event',value)
			event 自定义事件名称
			value 要传递的数据（可选参数）
		2、在发数据组件的标签里
			如
			<son @自定义事件名称="函数名"></son>
		3、在接受数据组件的methods里
			函数名（val）{
				val就是接受到的数据
			}

示例

	<template id="fatherT">
        <div>
            <h1>我是爸爸</h1>
            <p>儿子说：{{sonTalk}}</p>
            <son :hi='hello' @say='getSay'></son>
        </div>
    </template>
    <template id="sonT">
        <div>
            <h1>儿子</h1>
            <p>爸爸对你说：{{hi}}</p>
            <button @click='toFather'>看儿子怎么说</button>
        </div>
    </template>

	new Vue({
            el:"#app",
            components:{
                father:{
                    template:'#fatherT',
                    data() {
                        return {
                            hello:'崽子',
                            sonTalk:''
                        }
                    },
                    methods: {
                        getSay(data){
                            this.sonTalk=data
                        }
                    },
                    components:{
                        son:{
                            template:'#sonT',
                            data() {
                                return {
                                    sonSay:"儿子说：你是我老子"
                                }
                            },
                            props:['hi'],
                            methods: {
                                toFather(){
                                    this.$emit('say',this.sonSay);
                                }
                            },
                        }
                    }
                }
            }
        })

8、vue-cli vue脚手架的搭建
 	
	首先安装node.js
	可以先安装淘宝镜像可以加速下载脚手架
	$ npm install -g cnpm --registry=https://registry.npm.taobao.org
	用 cnpm -v 检验是否成功安装
	如果显示无法加载文件.....
	则用管理员的方式运行vscode
	执行 get-ExecutionPolicy，显示Restricted，表示状态是禁止的
	执行：set-ExecutionPolicy RemoteSigned
	这时再执行 get-ExecutionPolicy ，就显示RemoteSigned
	安装完成以后 下载安装vue -cli 
	cnpm install-g @vue/cli
	安装完成  创建 vue-cli
	把终端的路径转移到需要创建项目的路径里
	然后  vue create 项目名称      创建项目
	选择需要的项目
	成功后 cd到项目中  npm run serve  来启动项目

9、在脚手架中使用组件
	
	在一个组件里面是使用另一个组件，需要通过import...from的形式把件引进来
	import You from './components/You'
	export default {
		components:{  //导入进来的组件要放到components里面
    		You  //在es6里面，如果key与value相同，就可以省略一个 如You的具体写法 You:You
  		}
	}

10、生命周期函数
	
	1、beforeCreate  创建实例前触发
	2、created 		创建实例后触发
	3、beforeMount	渲染DOM前触发
	4、mounted		渲染DOM后触发
	5、beforeUpdate 	数据更改前触发
	6、updated 		数据更改后触发
	7、beforeDestroy	实例销毁前触发
	8、destroyed 	实例销毁后触发
	如果数据没有发生改动，5和6不会执行
	如果没有销毁，7和8不会执行
	
	
11、路由配置方法
	
路由配置方法一
	
	1、引入库
	2、定义路由，并对应router配置参数
		router：new VueRouter({
		routes:[
			{path:'路径'，compontent；'此路由对应组件'}
		]
	})
	3、使用<router-link>组件来导航，并通过to属性方法制定链接
	4、定义路由出口
	<router-view></router-view>
	
	路由重定向 （可以指定一个路由当做主页）
	this.$router.push('路径')
	
示例
	
	<div id="app">
        <ul>
            <li><router-link to="/Lin">林清玄</router-link></li>
            <li><router-link to="/Lu">鲁迅</router-link></li>
            <li><router-link to="/Yu">余华</router-link></li>
        </ul>
        <div class="box">
            <router-view></router-view>  //路由出口
        </div>
    </div>

	new Vue({
        el:'#app',
        beforeCreate() {
            this.$router.push('/Lin')  //重定向
        },
        router:new VueRouter({
            routes: [
                {path:'/Lin',component:{
                    template:'<h2>《白雪少年》<h2>'
                }},
                {path:'/Lu',component:{
                    template:'<h2>《呐喊》<h2>'
                }},
                {path:'/Yu',component:{
                    template:'<h2>《活着》<h2>'
                }}
            ]
        })
    })

路由配置方法二
	
	1、引入库
	2、定义路由组件
	3、定义路由
	4、创建router实例（路由对象），并对应router配置参数
	5、使用<router-link>组件来导航，并通过to属性方法制定链接
	6、定义路由出口
	<router-view></router-view>
	路由重定向
	 router.push('')

示例

	 //定义路由组件
        //三种不同的路由定义方法
        const Lin ={template:'<h2>《白雪少年》<h2>'}   
        const Lu =Vue.extend({
            template:'<h2>《呐喊》<h2>'
        })
        const Yu={template:'#yu'}
        //定义路由
        const routes=[
            {path:'/Lin',component:Lin},
            {path:'/Lu',component:Lu},
            {path:'/Yu',component:Yu}
        ]
        //创建router实例（路由对象），并对应router配置参数
        const router=new VueRouter({
            //把上面定义的路由放入
            routes
        })
        new Vue({
            el:'#app',
            router
        })
        //路由重定向
        router.push('/Lin')
    </script>

12、嵌套路由

	语法
	{path:'父级路由地址',component:'父级路由组件',children:[
		{path:'子级路由地址',component:'子级路由组件'}
	]}

示例 可以结合上一个

	const Winnie={template:'#win'}     
        //定义路由
        const routes=[
            {path:'/Lin',component:Lin},
            {path:'/Lu',component:Lu},
            {path:'/Yu',component:Yu,children:[
                {path:'winnie',component:Winnie}
            ]}
        	]

	<template id="yu">
        <div>
            <h2><router-link to="/Yu/Winnie">《活着》</router-link></h2>
            <router-view></router-view>
        </div>
    </template>

    <template id="win">
        <div>
            <li>dean</li>
            <li>winnie</li>
        </div>
    </template>

13、动态路由配置

	1、要匹配一个动态路由的话就用id，动态路径参数
	2、设置完后，参数值会被设置到this.$route.params

示例
	
	const Winnie={template:'<h2>winnie</h2>'}
        const Dean={template:'#d'}

        //点击某个郭后 要跳转到一个新的页面 ，所以也需要一个组件
        const deanList={template:'#dlist'}

        const routes=[
            {path:'/winnie',component:Winnie},
            {path:'/dean',component:Dean},
            {path:'/dean/:id',component:deanList}

        ]
        const router=new VueRouter({
            routes
        })

        new Vue({
            el:'#app',
            router
        })

	<div id="app">
        <ul>
            <li><router-link to="/winnie" >winnie</router-link></li>
            <li><router-link to="/dean">dean</router-link></li>
        </ul>
        <div class="box">
            <router-view></router-view>
        </div>
    </div>

    <template id="d">
        <div>
            <h2>dean</h2>
            <ul>
                <li><router-link to="/dean/1">郭1</router-link></li>
                <li><router-link to="/dean:2">郭2</router-link></li>
                <li><router-link to="/dean:3">郭3</router-link></li>
            </ul>
        </div>
    </template>

    <template id="dlist">
        <h3>id为:{{this.$route.params.id}}</h3>
    </template>

14、关于路由的一些知识点

	1、去掉路由导航中的#
	mode: 'history',
	2、设置当前点击的样式 前提是在css中已经设置了 active样式
	linkActiveClass:'active',
	3、指定跳转的标签 tage
	<router-link tag="div" to="/home">主页</router-link>
	4、用属性代替路由地址 ：to="属性名"
		属性名在data中设置
	5、给路由命名
	{path: '/Home',name:'homeLink',component: Home}
	<router-link :to="{name:'homeLink'}">主页</router-link>
	6、路由跳转方式
	回退：
		this.$router.go(-1);
	跳转到指定路由：
		1、this.$router.replace('/Home')
		2、this.$router.replace({name:'homeLink'})
		3、this.$router.push('/Home')
		4、this.$router.push({name:'homeLink'})
	7、错误路由的重定向
	{path:'*',redirect:'/Home'} 错误路由时重定向到首页

15、导航守卫

	1、全局守卫（在所有路由展示前触发）
	router.beforeEach((to,from,next)=>{//在引入router组件的页面里使用（main.js）
	to：即将要进入的路由，值为路由
	from 离开的路由（从哪个路由离开），值为路由
	next 值为函数，这个函数决定你接下来的路由页面
	})；

示例
	
	router.beforeEach((to,from,next)=>{
	if (to.path==='/Login'){
		next();
	}else{
    	alert('先登录'),
    	next('/Login')
		}
	})
	
	2、后置钩子
	router.afterEach((to,from)=>{//在引入router组件的页面里使用（main.js）
	to：即将要进入的路由，值为路由
	from 离开的路由（从哪个路由离开），值为路由
	})；

	3、路由独享的守卫
	beforeEnter(to,from,next){//在路由内部使用
	to：即将要进入的路由，值为路由
	from 离开的路由（从哪个路由离开），值为路由
	next 值为函数，这个函数决定你接下来的路由页面
	}；

示例
	
		{
	    path: '/Manage',
	    component: Manage,
	    beforeEnter: (to, from, next) => {
	      alert('laile')
	      next('/Login')
	    }   
	  },

	4、组件内的守卫(在组件内使用)
	beforeRouteEnter(to,from,next){
		//在当前路由被展示前使用
	}
	beforeRouteUpdate(to,from,next){
		//在当前路由改变时使用
	}
	beforeRouteLeave(to,from,next){
		//在离开当前路由前调用
	}
	
示例
	
	beforeRouteEnter(to,from,next){
        alert('lai');
        next(vm=>{
            alert(vm.name)
        })
    },
    beforeRouteLeave (to, from, next) {
        let answer=confirm('你确定要离开吗');
        if(answer){
            next()
        }else{
            next(false)
        }
    }

16、axios
	
	安装：npm install axios --save
	1、get请求
	this.$axios.get(url,{params:{key:value}})
	.then(
		res=>{
			请求成功回调函数
		}
	)
	.catch(
		err=>{
			//请求失败回调函数
		}
	)

示例
	
	this.$axios.get('http://rap2.taobao.org:38080/app/mock/251487/dean/19951025',{params:{name:'dean',age:18}})
				.then(
					res=>{
						console.log(res)
					}
				)
				.catch(
					err=>{
						console.log(err)		
					}
				)
	
	2、post请求
	this.$axios.get改成this.$axios.post其它参数不变

	3、另一种写法
	this.$axios({
			method:'post',
			url:'http://rap2.taobao.org:38080/app/mock/251487/dean/19951025',
			params:{  //  若是post以外的请求则把params改成data
				name:'dean',
				age:18
				}
			})
			.then(
				res=>{
					console.log(res)
				}
			)
			.catch(
				err=>{
					console.log(err)		
				}
			)
	
	
	