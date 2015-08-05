class: center,middle

# JavaScript 性能分析

王龑

[.fa.fa-github.big[]](https://github.com/wyvernnot/stuq_workshop)

---

# 新的应用

--

### Maker

- `cylon.js`

- mosca

--

### Docker

- `TravisCI`

--

- `is-docker`

--

- `打包`

--

- `DaoCloud`

---
class:middle
background-image: url(images/f1.jpg)

---

# 接下来将会介绍

### 1. Profile 
### 2. HeapSnapshot
### 3. GC

---

# Profile 的常见形式

- Sampling & Instrumentation

--

- 采样 & 插桩

---

# JavaScript 如何实现插桩

**`alert`函数**

```js
var _original=window.alert;

window.alert=function(){

    console.log('in');

    var result=_original.apply(this,arguments);

    console.log('out');

    return result;

}
```

---

# JavaScript 如何实现插桩

**`setTimeout`函数**

```js
var _original_sett = window.setTimeout;

window.setTimeout = function () {
    console.log('enter');

    var args = [].slice.apply(arguments);
    var _original_callback = args.shift();

    var callback = function () {
        console.log('exit');
        _original_callback.apply(this, arguments);
    }

    args.unshift(callback);

    var result = _original_sett.apply(this, args);
    return result;
}
```

---

background-image: url(images/trap.jpg)

---

class:center, inverse

![Xray of banana](images/banana.gif)

---

# Profilers

- Chrome Dev Tools

- Node-Inspector

- v8-profiler

---
class:middle,center

# \[DEMO\]

---

# 代码里开启 Profile

```js
console.profile('Profile1');

// your application

console.profileEnd('Profile1');
```

---

[01-abc.html](http://wyvernnot.github.io/stuq_workshop/example/01-abc.html)

.img[
![profile](images/profile-abc.png)
]


---

# Heap


---

# Heap 的组成

--SMI

---



