
### Mathematically structured computer programs

Slides for a talk to undergraduates given on 2011-02-28 introducting the idea of structuring a program with mathematics. The goal was to motivate and understand the category theory behind this small Haskell program

```haskell
import System.Environment

liftM           :: (Monad m) => (a -> b) -> m a -> m b
liftM f t       = t >>= (\y -> return (f y))

q               :: (Ord a) => [a]->[a]
q []            = []
q (x:xs)        = q [y|y<-xs,y<x] ++ [x] ++ q [y|y<-xs,y>=x]

main = (liftM q) getArgs >>= print
```

The slides give a brief introduction to category theory, monads, the list and state monads, and then in a handwavy way introduce the IO monad as a sort of state monad.

In the slides I wrote "Imagine trying to prove a theorem of mathematics which involves functions which are not well defined!" This is overly simplistic and conflates imperative with side-effecting. There is a big difference between imperative and impure. For instance one can go to any treatment of algorithms such as [Cormen et al](http://mitpress.mit.edu/books/introduction-algorithms) or [Kleinberg and Tardos](http://www.amazon.com/Algorithm-Design-Jon-Kleinberg/dp/0321295358) and find many mathematical theorems proved about what are for the most part pure functions written in an imperative style, notably making heavy use of destructive in place update.

Some of the students liked the idea that category theoretic ideas could be used to program a computer, and some just thought it was weird.

