# 导航菜单激活时添加 className

> 首页菜单使用`activeClassName`有一个BUG, 如果我点击了子页面时, `is-active`会一直存在, 并不会随着页面的切换而移除。    
> 下面就来看一下, 首页激活className处理办法。

```JavaScript
/**
 * 导航菜单
 *
 * @class Navbar
 * @extends React.Component
 */
class Navbar extends Component {
  constructor() {
    super();

    this.state = {
      activeClassName: 'is-active',
      isHome: false
    };
  }

  /**
   * 设置 this.state.isHome 为反值
   *
   * 传入 true, 返回 false
   * 传入 false, 返回 true
   *
   * @param {boolean} isHome
   */
  setIsHome(isHome) {
    this.setState({
      isHome: !isHome
    })
  }

  setHomeActive() {
    let { isHome } = this.state;
    let { pathname } = window.location;

    /**
     * 原理
     *
     * 当 isHome 为 true 时,
     * 给首页添加 `is-active` className
     * 否则移除
     *
     * 获取pathname, 判断 ^/$ 是否为 true,
     * 同时, 判断 isHome 值是否为 false;
     *     满足 则赋值 isHome 为 true;
     *
     * 否则
     * 判断 ^/$ 是否为 false,
     * 同时判断, isHome 值是否为 true;
     *     满足 则赋值 isHome 为 false;
     */
    if (
      ( new RegExp(/^\/$/).test(pathname) && !isHome ) ||
      ( !new RegExp(/^\/$/).test(pathname) && isHome )
    ) {
      this.setIsHome(isHome)
    }
  }

  /**
   * 刷新网页不会触发 `componentDidMount`, 但会触发 `componentDidUpdate`.
   */
  componentDidUpdate() {
    this.setHomeActive()
  }

  /**
   * 首次打开时, 渲染完毕后。
   */
  componentDidMount() {
    this.setHomeActive()
  }

  render() {
    const { activeClassName, isHome } = this.state;

    return (
      <div>
        <ul>
          <NavLink to="/" className={ isHome ? activeClassName : "" }>Home</NavLink>
          <NavLink to="/page" activeClassName={ activeClassName }>Page</NavLink>
        </ul>
      </div>
    )
  }
}
```
