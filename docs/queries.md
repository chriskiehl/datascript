# Return maps

```
return-map  = (return-keys | return-syms | return-strs)
return-keys = ':keys' symbol+
return-syms = ':syms' symbol+
return-strs = ':strs' symbol+
```

If you need a query to return a set of maps instead set of tuples, specify one of `:keys` / `:syms` / `:strs`, followed by a list of symbols:

```
[:find ?name ?age ?email, ...]
=> #{["Ivan" 10 "ivan@"]
     ["Oleg" 20 "oleg@"]
     ["Sergey" 30 "sergey@"]}

[:find ?name ?age ?email
 :keys name A e-mail
 ...]
=> #{{:name "Ivan",   :A 10, :e-mail "ivan@"}
     {:name "Oleg",   :A 20, :e-mail "oleg@"}
     {:name "Sergey", :A 30, :e-mail "sergey@"}}
```

`:strs` forces map to have string keys, `:syms` for symbols.

Return maps are only compatible with normal find and tuple-returning find:

```
[:find [?name ?age ?email], ...]
=> {:name "Ivan",   :A 10, :e-mail "ivan@"}
```

The amount of keys must match the amount of find elements.

Datomic docs: https://docs.datomic.com/on-prem/query.html#return-maps