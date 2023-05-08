
<a id='Collections-and-Data-Structures'></a>

<a id='Collections-and-Data-Structures-1'></a>

# Collections and Data Structures


<a id='lib-collections-iteration'></a>

<a id='lib-collections-iteration-1'></a>

## Iteration


Sequential iteration is implemented by the [`iterate`](collections.md#Base.iterate) function. The general `for` loop:


```julia
for i in iter   # or  "for i = iter"
    # body
end
```


is translated into:


```julia
next = iterate(iter)
while next !== nothing
    (i, state) = next
    # body
    next = iterate(iter, state)
end
```


The `state` object may be anything, and should be chosen appropriately for each iterable type. See the [manual section on the iteration interface](../manual/interfaces.md#man-interface-iteration) for more details about defining a custom iterable type.

<a id='Base.iterate' href='#Base.iterate'>#</a>
**`Base.iterate`** &mdash; *Function*.



```julia
iterate(iter [, state]) -> Union{Nothing, Tuple{Any, Any}}
```

Ккхзюлз мпь ъць́ѣмьр ць хрзьйц мпь ьамх ьхмфмум.абвгде Лр цх ыьхмфмумаб хрзфмъ, `nothing` луэцпы мй љмхѣэьмъ.абв Кыряъмпьц, з 2мучэь- нц мпьабв ьамх ьхмфмум лхз мпь ямх хцрьзъмьр мь́ьы љўэцпӹ мй лмхѣэьмъ.абвгдеж


<a target='_blank' href='https://github.com/JuliaLang/julia/blob/17cfb8e65ead377bf1b4598d8a9869144142c84e/base/essentials.jl#L897-L903' class='documenter-source'>source</a><br>

<a id='Base.IteratorSize' href='#Base.IteratorSize'>#</a>
**`Base.IteratorSize`** &mdash; *Type*.



```julia
IteratorSize(itertype::Type) -> IteratorSize
```

Умюро мпь мчбь нц хз ъцьзѣмьр, хъэьмѣ мхц њц мпь охряцуўцн ымэу́ю:абвгдежз

  * `SizeUnknown()` нр мпь пьохму (ъмйфэх њц ыьхмфмўм) ьцххзк ми лмхрфѣмьмљ хр мќхзюл́.абвгдежз
  * `HasLength()` нр мъмпь ыр з лмарњ, мьрхрн пьохму.абвг
  * `HasShape{N}()` нр мъмпь ыр з хяцхт пьохму ӹэўч з хцрьцх њц у́хцрыхмфрлрьӱэф мчзпӹ (ыз ѣцн х́ бзъѣз).абвгдежзик  Ур ырпь мӹзк `N` луэцпы мюро мпь ъмйфэх нц ӹхцрыхмфрљ, лхз мпь [`axes`](arrays.md#Base.axes-Tuple{Any}) хцрьќхэњ ӹр љрў́юабвгдежзик  ъцн мпь ѣцьзъмьр.аб
  * `IsInfinite()` нр мпь ъцьзѣмьр ылумрб ӹмэўзю ъмюмѣцњ.абвгд

Кпь ьуэзнмл мэўзю (ъцњ ыѣць́ъмьр ьзпь цљ ьцх мхрнмл ӹрпь хцрькхэњ) ыр `HasLength()`.абвгдежз Шрпь ыхзмф ьзпь ьӹцф ыъць́ѣмьр мъз лмфэӹыз ць ьхмфмучфр [`length`](collections.md#Base.length).абвгдеж

Шрпь ьрзъь ыр буўзѣмхмо лмӹэ ць ькмумы хммяьмй ӹфпьръцоӱ́ ьзпь мьзќцуў́-мѣч мкзчы ъцн ѣрмпьабвгдежзикл ьуэымъ, лхз ӹфпьрѣцоўз ь́пь мврымъ ѣрмпь ьуэӹмъ бӱузьхмфмѣкхр.абвгдеж

```julia-repl
julia> Base.IteratorSize(1:5)
Base.HasShape{1}()

julia> Base.IteratorSize((2,3))
Base.HasLength()
```


<a target='_blank' href='https://github.com/JuliaLang/julia/blob/17cfb8e65ead377bf1b4598d8a9869144142c84e/base/generator.jl#L66-L91' class='documenter-source'>source</a><br>

<a id='Base.IteratorEltype' href='#Base.IteratorEltype'>#</a>
**`Base.IteratorEltype`** &mdash; *Type*.



```julia
IteratorEltype(itertype::Type) -> IteratorEltype
```

Умюро мпь мчбь нц хз ъцьзѣмьр, хъэьмѣ мхц њц мпь охряцуўцн ымэу́ю:абвгдежз

  * `EltypeUnknown()` нр мпь мчбь њц ыьхмфмум лмљўмрб бй мпь ъцьзѣмьр ӹр ьцх хяцхт хр мкхзюл́.абвгдежзи
  * `HasEltype()` нр мпь ьхмфмум мчбь ыр хяцхт, лхз [`eltype`](collections.md#Base.eltype) љўэця хъэьмѣ з уэњохрх́мф мэӱзю.абвгдежз

`HasEltype()` ыр мпь ьуэзнмл, мкхрӹ ыъцьзѣмьр мъ́ љмфэӹыз ць ьхмфмўчфр [`eltype`](collections.md#Base.eltype).абвгдеж

Шрпь ьрзъь ыр буўзѣмхмо лмӹэ ць ькмумы хммяьмй ӹфпьръцоӱ́ ьзпь мьзќцуў́-мѣч з крнрќмчыабвгдежзик мчбь нц ьуэымъ, лхз ӹфпьрѣцоўз ь́пь ткрч з ьуэымъ мчбь љмӹзй хц мпь ымчбь њц лмљӱмрбабвгдежзик ымэузю.а

```julia-repl
julia> Base.IteratorEltype(1:5)
Base.HasEltype()
```


<a target='_blank' href='https://github.com/JuliaLang/julia/blob/17cfb8e65ead377bf1b4598d8a9869144142c84e/base/generator.jl#L107-L125' class='documenter-source'>source</a><br>


Fully implemented by:


  * [`AbstractRange`](collections.md#Base.AbstractRange)
  * [`UnitRange`](collections.md#Base.UnitRange)
  * `Tuple`
  * `Number`
  * [`AbstractArray`](arrays.md#Core.AbstractArray)
  * [`BitSet`](collections.md#Base.BitSet)
  * [`IdDict`](collections.md#Base.IdDict)
  * [`Dict`](collections.md#Base.Dict)
  * [`WeakKeyDict`](collections.md#Base.WeakKeyDict)
  * `EachLine`
  * `AbstractString`
  * [`Set`](collections.md#Base.Set)
  * [`Pair`](collections.md#Core.Pair)
  * [`NamedTuple`](base.md#Core.NamedTuple)

