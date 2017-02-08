What I want people to get out of this talk?
===========================================

I want to tell people about a different methodology of styling their websites that in some cases can help the maintainability of projects but of course it's possible that this way might not work for them at all.

Who am I addressing?
====================

Developers unfamiliar with functional CSS (or those that maybe they heard the name, but they are not sure how it works).

What's the general flow of the talk?
====================================

First, I will say why writing CSS is hard, then I will describe how functional CSS works and then list the good parts and bad parts of functional CSS.


Presentation:
* There is no one, ultimate and correct way to write CSS. Sooner or later, CSS will make you miserable and will become hard to maintain (so exactly like with JavaScript, except that for JS it happens way faster).
* What's the problem with CSS?:
    - The main problem is the "C" in CSS - it's cascading. It's a great idea that just doesn't scale and the bigger your code becomes, the more it gets in your way instead of helping you achieve your goals.
    - Hard to maintain - the bigger or longer the project, the more CSS is unused or duplicated. It's very hard to keep track of your CSS so developers end up adding even more CSS (let's face it, if you have thousands lines of CSS and you need add a new one, you will probably end up writing yet another class - why ? Because maybe there is a class with similar properties to what you need, but not really and you are not sure what will break when you try to modify it - so instead of checking everything by hand, you decide to create a new class).
        + Show an example of how the CSS for a large project looks like (something like here: https://github.com/chibicode/react-functional-css-protips#on-not-writing-new-css but maybe with a big website).
    - There are some tools that can help you a bit - the visual regression tests are a great idea, but from my experience they are way more difficult to make them work (the tooling is still getting there, but for example services like percy.io can be useful)
* So how can we solve this problem ?
    - One way is to use one of the methodologies that are supposed to help you keep the CSS maintainable (BEM for modularization of CSS, OOCSS). The problem with BEM is that you lose the dynamic aspect of CSS. If you want to have 2 types of buttons (small and large) and then you want to have two different colors of buttons (red and green), you would have to create a class for every combination (btn-small--green, btn-large--green, etc., although following the BEM methodology you would name them more semantically, like "navigation__button--green and article__button--red").
    - Or you could use the functional CSS - quite a new idea (got popular last year maybe?). Functional is now very trendy.
* The idea of functional CSS (or at that time, atomic CSS was first introduced in 2013 by Thierry Koblentz: https://www.smashingmagazine.com/2013/10/challenging-css-best-practices-atomic-approach/ and people hated it :) )
* *DESCRIBE HOW IT WORKS*
* It won't solve all your problems, but it might solve some of them.
* The advantages:
    - You can modify the existing styling for HTML elements without the fear that you will break something. If you decide that a given image no longer needs to float to the right, you remove '.float-right' class vs. checking what class that image had, checking what other places use the same class and then deciding if it should be removed or not. If you remove a class or a CSS rule, you need to check other places if everything still works fine (remember, it's **cascading**, so there can be consequences that you won't easily see). Which means that more often than not, developers will decide to leave the old CSS code there. It results in big CSS files, full of unused rules.
    - All classes have the same specificity level (which is just one class) - it will make modifications way easier (for example, if you want to include the left-to-right support you just add another CSS file that will overwrite some of the rules related to the text direction). Or if you decide that you want to have different color themes for your website - you just include small CSS file that overwrites some of the existing classes. Try doing that with bootstrap or one of the frameworks that use a lot of CSS combinations (*give an example*)
    - Once you learn the most common class names (and in most cases those are just simple abbreviations), you will be actually coding faster (need a div with small margin on top and black background? No problem, just add class="mt1 bg-black" and you are done).
    - It encourages you to split you HTML into components (or partials/mixins/widgets/blocks/whatever) which will make your code DRY. Also, Tachyons has a huge list of components that you can reuse: http://tachyons.io/components/
    - Styling you CSS with classes vs modifying CSS classes is cache-friendly (and you know that they say about cache invalidation).
    - Less CSS to download = website loads faster = better user experience. The functional CSS can be easily shareable between all sub-pages of your website, since it doesn't contain any content-specific rules.
* What are the problems of functional CSS?
    - The main problem is that it won't work with any other existing, non-functional frameworks, like bootstrap or foundation, and many websites use those frameworks as they give you a lot of styling out of the box. This is because bootstrap and other frameworks depends a lot on the cascading part of CSS, while functional CSS completely ignores the cascading in CSS
    - "So now I'm replacing duplicated CSS rules with duplicated CSS classes and instead of having messy CSS files I will have messy HTML files?" Well, yes. But sometimes it's a better solution. Some new(-ish) frameworks like React encourage componentization and reuse of HTML and in this case, the functional CSS might work very well. Still it might be a bit overwhelming to see a lot of classes in HTML, especially once you start adding additional, responsive classes (yet, it might still be easier to embrace it that a lot of CSS).
    - One of the main pains here will be updating existing components. Let's say you decide to change the font family and font size for a bunch of components on your website. Without non-functional CSS you could just open the CSS file and replace those variables in couple of places (or maybe even in just a handful of places if you use a CSS preprocessor like SASS or CSS variables). With functional CSS it gets a bit more complicated.
* So I won't have to write CSS anymore? No, you will still write CSS for stuff that can't be reusable (for example a box with 42px margin, 158px padding and font size of 17px, that will be pixel-perfect but it won't be reusable at all). Also, in my opinion, if you really want to have CSS classes with a set of rules, nothing stops you. You can create a generic element that you know you won't change often (if you do change it often, then you are back to the problems that we just tried to solve by using the functional CSS) and you want to reuse in multiple places. For example, if you want a modal for your website, just create:
```
.modal {
    position: fixed;
    top: 50%;
    left: 50%;
    -webkit-transform: translate(-50%,-50%);
    -ms-transform: translate(-50%,-50%);
    transform: translate(-50%,-50%);
    *width: 600px;
    *margin-left: -300px;
    *top: 50px;
}
```
then if you need a bigger modal, just add 'width-50' class (as long as you don't bump the selectors specificity, you shouldn't get into many troubles). Or to actually make it better, just add the styles that you know you won't need to overwrite and the add the remaining styles with functional classes (so width, margin left and top will come from different classes).
* Functional CSS is not a silver bullet (there is no silver bullet in CSS, there are just less painful ways of doing stuff), but it might solve some of the problems that you have. At the end when it comes to CSS it all boils down to the "CSS bloat vs HTML bloat" since you data has to live somewhere. At some point you will have to make a choice between:
`<div class="sidebar">` and `<div class="float-left margin-right-1 width-25` and there is no correct answer to that question.

Possible questions:
* "So why don't you just inline CSS like at the beginning of HTML times"/"It's just like inline styling"?
    - Because modifying inline CSS is tedious. Let say you decide that now the small margin is not 5px but 10 px. If you inline it, you now have to find all occurrences of that style and replace it. If you keep using classes, you just go to your CSS file and change the rule, for let's say ".margin-small". Or if you decide that now, the red class should no longer be #ff0000, but #ff1100. You can easily do this if you use CSS or Sass variables (and you should be using them!).
    - You can't use pseudo selectors or media queries.
    - Also, it's more typing.
* Is this thing responsive? *check the examples from tachyons for responsive classes*

What to check:
* What about active/hover pseudo selectors?
    - There are selectors for that, for example `.hover-black:hover` will change the color to black on hover. There are also libraries with hover effects that you can use: http://tachyons.io/docs/themes/hovers/ and other pseudo selectors (like nth for striped tables: https://github.com/tachyons-css/tachyons-tables). You can even do stuff like that if you like:
    .bg-red-500\:hover:hover {
     background-color: darken(red, 20%);
    }
    <p class=”bg-red-400 bg-red-500:hover”>
      Hipster ipsum obscure reference
    </p>
