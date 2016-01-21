# Android Bug 189121 example

This is an example App for [Android Bug 189121](https://code.google.com/p/android/issues/detail?id=189121).
The callback `onRequestPermissionsResult` isn't called in Nested Fragments. Instead the callback from the hosted Fragment is called. Which no one expected :)

## The original Bug tracker Bug description

> **Nested Fragment.requestPermissions / Deny or Allow / but no callback to Fragment.onRequestPermissionsResult**

> Steps:
>  1. Setup Frament with TabLayout&ViewPager and 2 nested fragments (used getChildFragmentManager() for setting up viewpager).
>
>  2. Nested Fragment.requestPermissions(new String[] {Manifest.permission.WRITE_EXTERNAL_STORAGE}, 1);
>
>  3. Click Allow or Deny
>
>  4. Observe that Nested Fragment.onRequestPermissionsResult is NOT called
>
> Expected behaviour: Nested Fragment.onRequestPermissionsResult should be called.

## About this example

I haven't exactly reproducted the steps above.
This example have an Activiy which hosted an Fragment via
```java
getSupportFragmentManager().beginTransaction().add(R.id.fragment_container, new FragmentInActivity()).commit();
```
The `FragmentInActivity` class contains also an Nested Fragment via the `ChildFragmentManager`
```java
getChildFragmentManager().beginTransaction().add(R.id.nested_fragment_container, new FragmentInFragment()).commit();
```

To verify the bug I've implemented in both Fragments the `onRequestPermissionsResult()` callback.
But only the callback from `FragmentInActivity` will be called.

