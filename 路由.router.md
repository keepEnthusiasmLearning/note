## Router Link

路由链接将被渲染为 `<a href='to'>` 标签。

	<router-link 
		to='/'
		replace 															// 调用 `router.replace()` 而非 `router.push()`
		active-class='activeClass'
		exact-active-class='exactActiveClass'	// 精准匹配时的类
		aria-current-value='aria-current'			// 激活时传递的值
		custom																// 不再渲染为链接，而是作为 v-slot 给库作者使用		
	>

	<router-link v-slot='{ href, route, navigate, isActive, isExactActive }'>

- href - 表示解析后的 URL
- route - 表示解析后的 route
- navigate - 触发导航的函数
- isActive - Boolean，是否应用 active class
- isExactActive - Boolean，是否应用 exact active class

## Router View

	<router-view 
		name='' 
		route 
		v-slot='{ Component, route }'
	>

## Vue Router API

	import { createRouter, useRoute, useRouter } from 'vue-router'

**实例化路由器**

	const VueRouter = createRouter(RouterOptions): Router

**返回路由器实例**

	const router = useRouter(): Router

**返回当前路由地址**	

	const route = useRoute(): RouteLocationNormalizedLoaded

## Router Instance

- `currentRoute` - RouteLocationNormalized，只读，当前路由地址
- `options` - RouterOptions，只读，创建时的配置对象。
	- `history` - 传入通过 API 创建的历史记录对象。
	- `linkActiveClass` - String，激活类
	- `linkExactActiveClass` - String，精确匹配时激活类 
	- `parseQuery`
	- `routes: Array<RouteRecordRaw>` - 初始的路由记录数组
	- `scrollBehavior` - 滚动行为
	- `stringifyQuery`

**方法**

- `addRoute(parentName: string | symbol, route: RouteRecordRaw): () => void` - 添加或覆盖一条路由记录。
- `afterEach((to, from, failure) => {})` - 添加导航守卫
- `back()` - 等同于 `router.go(-1)`
- `beforeEach((to, from, next) => {})	` - 添加导航守卫			
- `beforeResolve((to, from, next) => {})` - 添加导航守卫
- `forward()` - 等同于 `router.go(1)`
- `getRoutes(): RouteRecord[]` - 获取所有 路由记录的完整列表
- `go(n)` - 从当前跳转到 n 指定的历史记录位置。
- `hasRoute(name: string | symbol): boolean` - 检测是否存在指定路由器
- `isReady(): Promise<void>` - 完成初始化时调用，包括异步组件和异步钩子。
- `onError(callback)` - 路由错误时调用
- `push(location, onComplete?, onAbort?)` - 跳转到 to 指定位置，添加历史记录。
- `removeRoute(name: string | symbol): void` - 删除指定名称路由。
- `replace(location, onComplete?, onAbort?)` - 跳转到 to 指定位置，不添加历史记录。
- `resolve(location, current?, append?)` - 解析当前位置

## RouteLocationNormalizedLoaded 路由地址

- `fullPath` - 完整的路由地址 URL 编码。
- `path` - pathname 部分，即初始化时 `path` 属性定义部分。
- `hash` - `#` 开头的部分，
- `query` - search 部分，即跟随的参数。
- `matched` - RouteRecordNormalized[]，该地址匹配的路由记录数组。
- `meta` - 携带的元数据
- `name` - 路由名
- `redirectedFrom`
- `params` - 代表在 `path` 中以 `:` 定义的路径参数，例如：
	- `routers = [{path: '/users/:username/posts/:postId'}]`
	- `to='/users/eduardo/posts/123'`
	- `this.$route.params = { username: 'eduardo', postId: '123' }`


































































## 路由记录

**RouteRecordNormalized**

标准的路由记录类型

- `path` - 路由地址
- `redirect` - 重定向路由地址
- `name` - 路由记录名
- `aliasOf` - 作为另一记录的别名
- `children` - 子数组
- `beforeEnter` - 导航守卫
- `meta` - 传递的数据
- `props`
- `components` - Record<string, Component>，视图

**RouteRecordRaw**

在 `router options` 中或使用 `router.addRoute()` 时的路由记录类型。

- `path` - String，路由地址。`/`
- `redirect` - String | Location | Function，重定向路由地址。
- `name` - 路由名
- `alias` - 别名
- `children` - Array<routeOption>，路由嵌套
- `beforeEnter(to: Route, from: Route, next: Function) => void`
- `meta` - Any，元数据
- `props` - boolean | Object | Function
- `sensitive` - Boolean，匹配是否区分大小写
- `strict` - Boolean，严格检测 `/`

## RouterHistory 历史记录

传入实例化路由时的选项对象 RouterOptions history 字段

创建 HTML 5 历史记录，如：`https://example.com/folder/index`

	createWebHistory(base?: string): RouterHistory

- `base` - 提供开始路径的字符串，如：`/folder/`

创建 hash 历史记录，如：`https://example.com/folder/#index`

	createWebHashHashHistory(base?: string): RouterHistory

创建基于内存的历史记录。

	createMemoryHistory(base?: string): RouterHistory` - 

## 导航守卫

渲染组件前调用

	beforeRouteEnter(to, from, next) => {}

在渲染动态参数路由，组件被复用时调用

	beforeRouteUpdate(to, from) => {}	

离开该组件的路由时调用

	beforeRouteLeave (to, from)

**参数**

- `to` - 导航到达的路由地址。
- `from` - 导航到达之前的路由地址。
- `next` - Function，在组件渲染完成时执行的回调函数。

## 验证导航结果

`isNavigationFailure` - 验证导航失败的函数。
`NavigationFailureType` - 包含失败类型的杖举。

	import { NavigationFailureType, isNavigationFailure } from 'vue-router'

	const failure = await router.push('/articles/2')

	if (isNavigationFailure(failure, NavigationFailureType.aborted)) {
		// do something
	}






















## START_LOCATION

路由器的初始路由位置。可用在导航守卫中使用来区分初始导航。

	import { START_LOCATION } from 'vue-router'

	router.beforeEach((to, from) => {
	  if (from === START_LOCATION) {
	    // 初始导航
	  }
	})