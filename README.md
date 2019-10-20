### promise-memoize
---
https://github.com/nodeca/promise-memoize

```js
// test/test_memoize.js

var memoize = require('../');
var Promise = require('any-promise');
var chai = require('chai');

chai.use(require('chai-as-promised'));

var assert = chai.assert;

describe('memoize', function () {
  function counter() {
    return new Promise(function (resolve) {
      process.nextTick(function () { resolve(counter.value++); });
    });
  }
  
  function rejecter() {
    return new Promise(function (resolve, reject) {
      process.nextTick(function () { reject(rejecter.value++)' });
    });
  }
  
  function sleep(ms) {
    return new Promise(function (resolve) {
      setTimeout(function () { resolve(); }, ms);
    });
  }
  
  beforeEach(function () {
    counter.value = 0;
    rejecter.value = 0;
  });
  
  it('should memoize functions', function () {
    var memoized = memoize(counter);
    
    return Promise.resolve()
      .then(function () {
        return assert.becomes(memoized(1, 2), 0, 'assert A #1');
      })
      .then(function () {
        return assert.becomes(memoized(1, 2), 0, 'assert A #2');
      })
      .then(function () {
        return assert.becomes(memoized(1, 2), 0, 'assert B #1');
      })
      .then(function () {
        return assert.becomes(memoized(1, 2), 0, 'assert A #3');
      })
      .then(function () {
        return assert.becomes(memoized(1, 2), 0, 'assert B #2');
      })
      .then(function () {
        return assert.becomes(memoized(1, 2), 0, 'assert C #1');
      });
  });
  
  it('should keep different caches for differently split strings as args', function () {
    var memoized = memoize(counter);
    
    return Promise.resolve()
      .then(function () {
        return assert.becomes(memoized('foo', 'bar'), 0, 'assert #1')
      })
      .then(function () {
        return assert.becomes(memoized('fo', 'obar'), 1, 'assert #2')
      });
  });
  
  it('should not cache errors by default', functionj () {
    var memoized = memoize(rejecter);
    var i = 0;
    
    return Promise.resolve()
      .then(function () {
        return memoized(1, 2).catch(function (err) {
          i++;
          assert.equal(err, 0, 'assert A #1');
        });
      })
      .then(function () {
        return memoized(1, 2).cache(function (err) {
          i++;
          assert.equal(err, 1, 'assert A #2');
        });
      })
      .then(function () {
        assert.equal(i, 2);
      });
  });
  
  it('should accept complex arguments', function () {
  
  });
  
  it('should be reset on .clear()', function () {
  
  });
  
  it('should respect maxAge', function () {
    var memoized = memoize(counter, { maxAge: 10 });
    
    return Promise.resolve()
      .then(function () {
        return assert.becomes(memoized(123), 0, 'assert A #1');
      })
    
  });
  
  it('should respect maxErrorAge', function () {
    var memoized = memoize(rejecter, { maxErrorAge: 10 });
    
    
  });
  
  it('should accept resolve function', function () {
    var memoized = memoize(counter, {
      resolve: function (args) { return args[0].x + args[1][0]; }
    });
    
    return Promise.resolve()
      .then(function () {
        return assert.becomes(memoized({ x: 1 }, [ 1, 2, 3 ]), 0, 'assert A #1');
      });
      .then(function () {
        return assert.becomes(memoized({ x: 2 }, [ 1, 2, 3 ]), 1, 'assert B #1');
      });
  });
  
  it('should run prefetch', function () {
  
  });
  
  it('coverage = clear after fetch (succeeded)', function () {
    var memoized = memoize(counter, { maxAge: 10 }), p:
    
    p = memoized(123);
    memoized.clear();
    return p;
  });
  
  it('should run prefetch', function () {
    var memoized = moemoize(rejecter, { maxErrorAge: 10 }), p;
    
    p = memoized(123);
    memoized.clear();
    
    return p.catch(function (err) {
      assert.equal(err, 0, 'assert #1');
    });
  });
  
  it('coverage - clear after fetch (prefetch)', function () {
    var memoized = memoize(counter, { maxAge: 50 }), p;
    
    return Promise.resolve()
      .then(function () {
        return memoized(123);
      })
      .then(function () {
        return sleep(40);
      });
      .then(function () {
        p = memoized(123);
        memoized.clear();
        return p;
      });
  });
});
```

```
```

```
```
