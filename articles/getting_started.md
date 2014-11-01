---
title: "Getting Started with Reagent"
layout: article
---

# Getting Started

## Introduction to Reagent

Reagent provides a minimalistic interface between ClojureScript and React. It allows you to define efficient React components using nothing but plain ClojureScript functions and data, that describe your UI using a Hiccup-like syntax.

The goal of Reagent is to make it possible to define arbitrarily complex UIs using just a couple of basic concepts, and to be fast enough by default that you rarely have to care about performance.

A very basic Reagent component may look something like this:

{% highlight clojure %}
(defn simple-component []
  [:div
   [:p "I am a component!"]
   [:p.someclass
    "I have " [:strong "bold"]
    [:span {:style {:color "red"}} " and red "] "text."]])
{% endhighlight %}

Which generates these DOM elements.

{% highlight html %}
<div>
  <p>I am a component!</p>
  <p class="someclass">I have <strong>bold</strong><span style="color:red;">and red </span>text.</p>
</div>
{% endhighlight %}

### Composition

You can build new components using other components as building blocks. Like this:

{% highlight clojure %}
(defn simple-parent []
  [:div
   [:p "I include simple-component."]
   [simple-component]])
{% endhighlight %}

To generate these DOM elements.

{% highlight html %}
<div>
  <p>I include simple-component.</p>
  <div>
    <p>I am a component!</p>
    <p class="someclass">I have <strong>bold</strong><span style="color:red;">and red </span>text.</p>
  </div>
</div>
{% endhighlight %}

### Passing Data

Data is passed to child components using plain old Clojure data types. Like this:

{% highlight clojure %}
(defn hello-component [name]
  [:p "Hello, " name "!"])

(defn say-hello []
  [hello-component "world"])
{% endhighlight %}

Example:

{% highlight html %}
<p>Hello, world!</p>
{% endhighlight %}

**Note:** In the example above, hello-component might just as well have been called as a normal Clojure function instead of as a Reagent component, i.e with parenthesis instead of square brackets. The only difference would have been performance, since ”real” Reagent components are only re-rendered when their data have changed. More advanced components though (see below) must be called with square brackets.

Here is another example that shows items in a seq:

{% highlight clojure %}
(defn lister [items]
  [:ul
   (for [item items]
     ^{:key item} [:li "Item " item])])

(defn lister-user []
  [:div
   "Here is a list:"
   [lister (range 3)]])
{% endhighlight %}

Example:

{% highlight html %}
<div>
 Here is a list:
    <ul>
      <li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
    </ul>
</div>
{% endhighlight %}

**Note:** The ^{:key item} part above isn’t really necessary in this simple example, but attaching a unique key to every item in a dynamically generated list of components is good practice, and helps React to improve performance for large lists. The key can be given either (as in this example) as meta-data, or as a :key item in the first argument to a component (if it is a map). See React’s documentation for more info.

### Managing State


