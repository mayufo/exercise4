# 练习4


## test1

```
describe('this', function () {
  it('setTimeout', function (done) {
    var obj = {
      say: function () {
        setTimeout(() => {
          // this 是什么？想想为什么？
          this.should.equal(obj)
          done()
        }, 0)
      }
    }
    obj.say()
  }) 
```

`setTimeout`在一般函数中`this`指向`window`,而这里用到了箭头函数(lambda表达式)

因此`setTimeout`函数外的`this`和`setTimeout`函数内的`this`是一样的，指向相同。
`setTimeout`函数外的this指向obj,因此`setTimeout`函数内的this也是指向`obj`

## test2

```
it('global', function () {
    function test() {
      // this 是什么？想想为什么？
      this.should.equal(global)
    }
    test()
  })
```

没有指定`this`,指向`window`,因为是在`node`环境下，这里指向`global`

## test3

```
  describe('bind', function () {
    it('bind undefined', function () {
      var obj = {
        say: function () {
          function _say() {
            // this 是什么？想想为什么？
            this.should.equal(global)
          }
          return _say.bind(obj)
        }()
      }
      obj.say()
    })
```

`bind`、`call`和`apply`都是改变函数`this`

此处的`obj`因为变量提升，开始为`obj = undefined`,因此在这个函数中`bind(obj)`，实际`bind(undefined)`

在没有指明`this`的情况下，this指向`global`

## test4

```js
it('bind normal', function () {
      var obj = {}
      obj.say = function () {
        function _say() {
          // this 是什么？想想为什么？
          this.should.equal(obj)
        }
        return _say.bind(obj)
      }()
      obj.say()
    })
```

开始定义了对象,为引用类型再运行，这里obj指向的就是obj,因此this也指向obj


