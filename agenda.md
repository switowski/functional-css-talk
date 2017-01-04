* Problem z css jest "cascading" part
* Ciężko jest stwierdzić czy zmiana jednej właściwości nie rozpieprzy css na innej stronie. Tutaj trochę moze pomoc visual testing (percy.io)
* Przez to tworzymy bardzo dużo klas, niektore z nich moga przestać być używane i nawet tego nie zauważymy.
* BEM trochę pomaga z ilością klas ale to jeszcze nie to.
* Lepsze rozwiązanie to functional css
* Może ono niestety spowodowac zbyt dużo klas
* Ale mimo to warto
* Moim zdaniem warto połączyć oba rozwiązania, stworzyc komponenty które mają zestaw właściwości (np button) ale używać też klas do marginesow, paddingow, border, font size etc.

Topics to discuss
* What's the problem with CSS?:
    - The main problem is the "C" in CSS - it's cascading. It's a great idea that just doesn't scale and the bigger your code becomes, the more it gets in your way instead of helping you achieve your goals.
    - Hard to maintain - the bigger or longer the project, the more CSS is unused or duplicated. It's very hard to keep track of your CSS so developers end up adding even more CSS (let's face it, if you have thousands lines of CSS and you need add a new one, you will probably end up writing yet another class - why ? Because maybe there is a class with similar properties to what you need, but not really and you are not sure what will break when you try to modify it - so instead of checking everything by hand, you decide to create a new class)
    - There are some tools that can help you a bit - the visual regression tests are a great idea, but from my experience they are way more difficult to make them work (the tooling is still getting there, but for example services like percy.io can be useful)
* So how can we solve this problem ?
    - One way is to use one of the methodologies that are supposed to help you keep the CSS maintainable (BEM for modularization of CSS, OOCSS).
    - Or you could use the functional CSS - quite a new idea (got popular last year maybe?). Functional is now very trendy.

* It won't solve all your problems, but it might solve some of them.
* The main problem is that it won't work with any other existing, non-functional frameworks, like bootstrap or foundation, and many websites use those frameworks as they give you a lot of styling out of the box.

Topics in order: