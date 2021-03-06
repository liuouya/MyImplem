#when metaprogramming
- compile time only
- can't reply on: mutability, virtual functions, other RTTI, etc

#some technics
- metafunction member types, static const data members, and constexpr member functions to express intermediate and final metafunction results. [abs](abs.cpp) [gcd](gcd.cpp)
- metafunction calls (possibly recursive), inheritance, and aliasing to factor commonalities. [rank](rank.cpp) [rank_revised](rank_revised.cpp)
- template specializations (complete and partial) for metafunction argument pattern-matching. [type_traits](type_traits.cpp)
- variadic template and parameter pack. [is_one_of](is_one_of.cpp)
- SFINAE to direct overload resolution. [type_traits](type_traits.cpp) [more_type_traits](more_type_traits.cpp)
- unevaluated oeprands, such as function calls to map types. [more_type_traits](more_type_traits.cpp)
- recent and classical std::metafunctions in \<type_traits>, \<iterator>, \<numeric_limits>, etc. [example](example.cpp)
- void_t. [example](example.cpp)

#some conventions
- if your metafunction has a type result, aliase it to "type"
- if your metafunction has a value result, aliase it to "value"
- note the evolution of value returning metafunction calls:
```
  is_void<T>::value   // since technical report 1
  bool(is_void<T>{})  // instantiate/cast, since c++11
  is_void<T>{}()      // instantiate/call, since c++14
  is_void_v<T>        // a c++14 variable template, since c++17
```
#unevaluated context
- sizeof, typeid, decltype, noexcept are never evaluated, not even at compile time
- which means, no code is generated for such operands
- which means, we need only a declaration, not a definition to use a name in these context
- an unevaluated function call (e.g. to foo) can usefully map one type to another
- decltype( foo(declval\<T>()) ), gives foo's return type were it called with a T rvalue
- the unevaluated call std::declval\<T>() is declared to give an rvalue result of type T. (std::decltype\<T&>() gives lvalue)


#constexpr
---> comes from abstract algebra :grinning:

##reference
- CppCon 2014: Walter E. Brown "Modern Template Metaprogramming: A Compendium, Part I" https://www.youtube.com/watch?v=Am2is2QCvxY
- CppCon 2014: Walter E. Brown "Modern Template Metaprogramming: A Compendium, Part II" https://www.youtube.com/watch?v=a0FliKwcwXE
