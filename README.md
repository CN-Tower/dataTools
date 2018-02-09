# FuncLib

A data processing methods lib of python.

## About
     Author: @CN-Tower
    Version: V2.0.0
  Create At: 2018-2-2
  Update At: 2018-2-10
     GitHub: http://github.com/CN-Tower/FuncLib

## Quick Start
```
$ pip install funclib
$ python
>>> from funclib import T
>>> T.help()
```
## Methods
 * [T.info    ](#tinfo)
 * [T.index   ](#tindex)
 * [T.find    ](#tfind)
 * [T.filter  ](#tfilter)
 * [T.reject  ](#treject)
 * [T.reduce  ](#treduce)
 * [T.contains](#tcontains)
 * [T.flatten ](#tflatten)
 * [T.each    ](#teach)
 * [T.uniq    ](#tuniq)
 * [T.drop    ](#tdrop)
 * [T.pluck   ](#tpluck)
 * [T.every   ](#tevery)
 * [T.some    ](#tsome)
 * [T.list    ](#tlist)
 * [T.dump    ](#tdump)
 * [T.clone   ](#tclone)
 * [T.test    ](#ttest)
 * [T.replace ](#treplace)
 * [T.iscan   ](#tiscan)
 * [T.log     ](#tlog)
 * [T.timer   ](#ttimer)
 * [T.now     ](#tnow)
 * [T.help    ](#thelp)

## Document

### T.info
```
    ===================================================================================
                                        Func-Lib
                        A data processing methods lib for Python(2/3)
    -----------------------------------------------------------------------------------
                                 Author: @CN-Tower
                              Create At: 2018-2-2
                              Update At: 2018-2-10
                                Version: V2.0.0
                                 GitHub: http://github.com/CN-Tower/FuncLib
    -----------------------------------------------------------------------------------
                          0: T.info                 1: T.index
                          2: T.find                 3: T.filter
                          4: T.reject               5: T.reduce
                          6: T.contains             7: T.flatten
                          8: T.each                 9: T.uniq
                         10: T.drop                11: T.pluck
                         12: T.every               13: T.some
                         14: T.list                15: T.dump
                         16: T.clone               17: T.test
                         18: T.replace             19: T.iscan
                         20: T.log                 21: T.timer
                         22: T.now                 23: T.help
    ===================================================================================
```
### T.index
```
    Looks through the list and returns the item index. If no match is found,
    or if list is empty, -1 will be returned.
    eg:
        from funclib import T
        persons = [{"name": "Tom", "age": 12},
            {"name": "Jerry", "age": 20},
            {"name": "Mary", "age": 35}]

        Jerry_idx = T.index({"name": 'Jerry'}, persons)
        Mary_idx  = T.index(lambda x: x['name'] == 'Mary', persons)

        print(Jerry_idx)  # => 1
        print(Mary_idx)   # => 2

```
### T.find
```
    Looks through each value in the list, returning the first one that passes
    a truth test (predicate), or None.If no value passes the test the function
    returns as soon as it finds an acceptable element, and doesn't traverse
    the entire list.
    eg:
        from funclib import T
        persons = [{"name": "Tom", "age": 12},
            {"name": "Jerry", "age": 20},
            {"name": "Mary", "age": 35}]

        Jerry = T.find({"name": 'Jerry'}, persons)
        Mary  = T.find(lambda x: x['name'] == 'Mary', persons)

        print(Jerry)  # => {'age': 20, 'name': 'Jerry'}
        print(Mary)   # => {'age': 35, 'name': 'Mary'}

```
### T.filter
``` 
    Looks through each value in the list, returning an array of all the values that
    pass a truth test (predicate).
    eg:
        from funclib import T
        persons = [{"name": "Tom", "age": 20},
                   {"name": "Jerry", "age": 20},
                   {"name": "Jerry", "age": 35}]

        Jerry = T.filter({"age": 20}, persons)
        Mary = T.filter(lambda x: x['name'] == 'Jerry', persons)
        print(Jerry)  # => [{'age': 20, 'name': 'Tom'}, {'age': 20, 'name': 'Jerry'}]
        print(Mary)   # => [{'age': 20, 'name': 'Jerry'}, {'age': 35, 'name': 'Jerry'}]
        
```
### T.reject
``` 
    Returns the values in list without the elements that the truth test (predicate) passes.
    The opposite of filter.
    eg:
        from funclib import T
        persons = [{"name": "Tom", "age": 12},
                   {"name": "Jerry", "age": 20},
                   {"name": "Mary", "age": 35}]

        not_Mary = T.reject({"name": "Mary"}, persons)
        adults = T.reject(lambda x: x['age'] < 18, persons)

        print(not_Mary)  # => [{"age": 12, "name": "Tom"}, {"age": 20, "name": "Jerry"}]
        print(adults)    # => [{"age": 20, "name": "Jerry"}, {"age": 35, "name": "Mary"}]

```
### T.reduce
```
    Returns the buildIn method 'reduce', in python 3 the 'reduce' is imported from functools.
    eg:
        from funclib import T
        num_list = [1 , 2, 3, 4]
        print(T.reduce(lambda a, b: a + b, num_list))  # => 10

```
### T.contains
```
    Returns true if the value is present in the list.
    eg:
        from funclib import T
        persons = [{"name": "Tom", "age": 12},
                   {"name": "Jerry", "age": 20},
                   {"name": "Mary", "age": 35}]

        is_contains_Jerry = T.contains({"name": "Jerry", "age": 12}, persons)
        is_contains_Mary = T.contains(lambda x: x['name'] == 'Mary', persons)

        print(is_contains_Jerry)  # => False
        print(is_contains_Mary)   # => True

```
### T.flatten
```
    Flattens a nested array (the nesting can be to any depth). If you pass shallow,
    the array will only be flattened a single level.
    eg:
        from funclib import T
        flt_list_01 = T.flatten([1, [2], [3, [[4]]]])
        flt_list_02 = T.flatten([1, [2], [3, [[4]]]], True)
        print (flt_list_01)  # => [1, 2, 3, [[4]]]
        print (flt_list_02)  # => [1, 2, 3, 4];

```
### T.each
```
    Produces a new values list by mapping each value in list through a transformation
    function (iteratee).
    eg:
        from funclib import T
        num_list = [1 , 2, 3, 4]
        list_10 = T.each(lambda x: x % 2, num_list)
        print(list_10)  #=> [1, 0, 1, 0]

```
### T.uniq
```
    Produces a duplicate-free version of the array.
    In particular only the first occurence of each value is kept.
    eg:
        from funclib import T
        persons00 = ("Tom", "Tom", "Jerry")
        persons01 = ["Tom", "Tom", "Jerry"]
        persons02 = [{"name": "Tom", "age": 12, "sex": "m"},
                     {"name": "Tom", "age": 20, "sex": "m"},
                     {"name": "Mary", "age": 35, "sex": "f"}]
        demo_list = [False, [], False, True, [], {}, False, '']

        unique_persons00 = T.uniq(persons00)
        unique_persons01 = T.uniq(persons01)
        unique_demo_list = T.uniq(demo_list)
        one_Tom = T.uniq({"name": "Tom"}, persons02)
        one_mail = T.uniq(lambda x: x['sex'] == "m", persons02)

        print(unique_persons00)  # => ["Jerry", "Tom"]
        print(unique_persons01)  # => ["Jerry", "Tom"]
        print(unique_demo_list)  # => [False, [], True, {}, '']
        print(one_Tom)  # => [{'age': 12, 'name': 'Tom', 'sex': 'm'}, {'age': 35, 'name': 'Mary', 'sex': 'f'}]
        print(one_mail)  # => [{'age': 12, 'name': 'Tom', 'sex': 'm'}, {'age': 35, 'name': 'Mary', 'sex': 'f'}]

```
### T.drop
```
    Delete false values expect 0.
    eg:
        from funclib import T
        tmp_list = [0, '', 3, None, [], {}, ['Yes'], 'Test']
        drop_val = T.drop(tmp_list)
        drop_val_and_0 = T.drop(tmp_list, True)

        print(drop_val)        # => [0, 3, ['Yes'], 'Test']
        print(drop_val_and_0)  # => [3, ['Yes'], 'Test']

```
### T.pluck
```
    Pluck the list element of collections.
    eg:
        from funclib import T
        persons = [{"name": "Tom", "hobbies": ["sing", "running"]},
            {"name": "Jerry", "hobbies": []},
            {"name": "Mary", "hobbies": ['hiking', 'sing']}]

        hobbies = T.pluck(persons, 'hobbies')
        hobbies_uniq = T.pluck(persons, 'hobbies', uniq=True)

        print(hobbies)      # => ["sing", "running", 'hiking', 'sing']
        print(hobbies_uniq) # => ["sing", "running", 'hiking']

```
### T.every
```
    Returns true if all of the values in the list pass the predicate truth test.
    Short-circuits and stops traversing the list if a false element is found.
    eg:
        from funclib import T
        tmp_list = [0, '', 3, None]
        persons = [{"name": "Tom", "age": 12, "sex": "m"},
                   {"name": "Jerry", "age": 20, "sex": "m"},
                   {"name": "Mary", "age": 35, "sex": "f"}]

        every_true = T.every(True, tmp_list)
        is_all_male = T.every(lambda x: x['sex'] == "m", persons)
        print(every_true)   # => False
        print(is_all_male)  # => False

```
### T.some
```
    Returns true if any of the values in the list pass the predicate truth test.
    Short-circuits and stops traversing the list if a true element is found.
    eg:
        from funclib import T
        tmp_list = [0, '', 3, None]
        persons = [{"name": "Tom", "age": 12, "sex": "m"},
                   {"name": "Jerry", "age": 20, "sex": "m"},
                   {"name": "Mary", "age": 35, "sex": "f"}]

        some_true = T.some(True, tmp_list)
        is_some_female = T.some(lambda x: x['sex'] == "f", persons)

        print(some_true)       # => True
        print(is_some_female)  # => True

```
### T.list
```
    Return now system time.
    eg:
        from funclib import T
        print(T.list())       # => []
        print(T.list([]))     # => []
        print(T.list({}))     # => [{}]
        print(T.list(None))   # => [None]
        print(T.list('test')) # => ['test']

```
### T.dump
```
    Return a formatted json string.
    eg:
        from funclib import T
        persons = [{"name": "Tom", "hobbies": ["sing", "running"]},
            {"name": "Jerry", "hobbies": []}]
        print(T.dump(persons)) #=>
        [
          {
            "hobbies": [
              "sing",
              "running"
            ],
            "name": "Tom"
          },
          {
            "hobbies": [],
            "name": "Jerry"
          }
        ]

```
### T.clone
```
    Create a deep-copied clone of the provided plain object.
    eg:
        from funclib import T
        persons = [{"name": "Tom", "age": 12}, {"name": "Jerry", "age": 20}]
        persons_01 = persons
        persons_02 = T.clone(persons)
        T.find({'name': 'Tom'}, persons)['age'] = 18
        print(persons_01)  # => [{"name": "Tom", "age": 18}, {"name": "Jerry", "age": 20}]
        print(persons_02)  # => [{"name": "Tom", "age": 12}, {"name": "Jerry", "age": 20}]

```
### T.test
```
    Check is the match successful, a boolean value will be returned.
    eg:
        from funclib import T
        not_in = T.test(r'ab', 'Hello World!')
        in_str = T.test(r'll', 'Hello World!')
        print(not_in)  # => False
        print(in_str)  # => True

```
### T.replace
```
    Replace sub string of the origin string with re.sub()
    eg:
        from funclib import T
        info = 'Hello I'm Tom!'
        print(T.replace('Tom', 'Jack', info))  # => True

```
### T.iscan
```
    Test is the expression valid, a boolean value will be returned.
    eg:
        from funclib import T
        print(T.iscan(int('a')))  # => False
        print(T.iscan(int(5)))  # => True

```
### T.log
```
    Show log clear in console.
    eg:
        from funclib import T
        T.log([{"name": "Tom", "hobbies": ["sing", "running"]}, {"name": "Jerry", "hobbies": []}])

        # =>
        ===========================================================================
                                    FuncLib ( V2.0.0 )
        ---------------------------------------------------------------------------
        [
          {
            "hobbies": [
              "sing",
              "running"
            ],
            "name": "Tom"
          },
          {
            "hobbies": [],
            "name": "Jerry"
          }
        ]
        ===========================================================================

```
### T.timer
```
    Set a timer with interval and timeout limit.
    eg:
        from funclib import T
        count = 0
        def fn():
            global count
            if count == 4:
                return True
            count += 1
            print(count)
        T.timer(fn, 10, 2)
        # =>
            >>> 1  #at 0s
            >>> 2  #at 2s
            >>> 3  #at 4s
            >>> 4  #at 4s

```
### T.now
```
    Return now system time.
    eg:
        from funclib import T
        print(T.now()) # => '2018-2-1 19:32:10'

```
### T.help
```
    Return the FuncLib or it's method doc
    eg:
        from funclib import T
        T.help('index')
        # =>
    ===========================================================================
                            FuncLib ( V2.0.0 ) --> T.index
    ---------------------------------------------------------------------------
        Looks through the list and returns the item index. If no match is found,
        or if list is empty, -1 will be returned.
        eg:
            from funclib import T
            persons = [{"name": "Tom", "age": 12},
                {"name": "Jerry", "age": 20},
                {"name": "Mary", "age": 35}]

            Jerry_idx = T.index({"name": 'Jerry'}, persons)
            Mary_idx  = T.index(lambda x: x['name'] == 'Mary', persons)

            print(Jerry_idx)  # => 1
            print(Mary_idx)   # => 2
    ===========================================================================

```
