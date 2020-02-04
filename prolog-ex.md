```prolog
% 23 Ancestry rules
sisters(X, Y) :- sibling(X, Y), female(X), female(Y).

uncle_nephew(X, Y) :- sibling(X, Z), parent_child(Z, Y), male(X), male(Y).

gparent_gchild(X, Y) :- parent_child(X, Z), parent_child(Z, Y).

% 24 Recursive rules
next(b, a).
next(c, b).
next(d, c).
after(X, Y) :- next(X, Y).
after(X, Y) :- next(X, Z), after(Z, Y).

prefix([], _).
prefix([X|Xs], [X|Ys]) :- prefix(Xs, Ys).

% 25 Relational thinking
% natural number
n(0).
n(s(X)) :- n(X).

% greater than or equal to
gte(X, 0) :- n(X).
gte(s(X), s(Y)) :- gte(X, Y).

% plus
myplus(0, X, X) :- n(X).
myplus(s(X), Y, s(Z)) :- myplus(X, Y, Z).

% --

% 26
suffix(Xs, Xs).
suffix(Xs, [_|Ys]) :- suffix(Xs, Ys).

append([], Ys, Ys).
append([X|Xs], Ys, [X|Zs]) :- append(Xs, Ys, Zs).

% [... x ...]
% [xs ... ys]
% [... xs]

% 27 curry

factorial(0,1).

factorial(N,F) :-  
   N>0, 
   N1 is N-1, 
   factorial(N1,F1), 
   F is N * F1.

% 29-1
sum(1,1).
sum(N,S) :-
    N>1,
    N1 is N-1,
    sum(N1,S1),
    S is N + S1.

% 29-2
power(_,0,1).
power(X,Y,P) :-
    Y>0,
    Y1 is Y-1,
    power(X,Y1,P1),
    P is X * P1.

% 30 optimize w/ cuts
partition([],_,[],[]) :- !.
partition([X|Xs],Pivot,Smaller,[X|Bigger]) :-
    X>Pivot,
    !,
    partition(Xs,Pivot,Smaller,Bigger).
partition([X|Xs],Pivot,[X|Smaller],Bigger) :-
    Pivot>X,
    !,
    partition(Xs,Pivot,Smaller,Bigger).


% 1 maximum
maximum(X,Y,Y) :- X<Y.
maximum(X,Y,X) :- X>=Y.

maximum2(X,Y,Y) :- X<Y, !.
maximum2(X,Y,X) :- X>=Y, !.

% 2 Fibonacci numbers
% functor s
myplus(X,0,X).
myplus(X,s(Y),s(Z)) :- myplus(X,Y,Z).

fibo(0,0).
fibo(s(0), s(0)).
fibo(s(s(X)), F) :- fibo(X,F2),
		    fibo(s(X),F1),
		    plus(F2,F1,F).

% is
fibo2(0,0).
fibo2(1,1).
fibo2(N,F) :- N>1,
	      N1 is N-1,
	      N2 is N-2,
	      fibo2(N1, F1),
	      fibo2(N2, F2),
	      F is F1+F2.

% 3 Modulo, gcd
mod(X,Y,X) :- Y > X.
mod(X,Y,R) :-
    X >= Y,
    X1 = X-Y,
    mod(X1,Y,R1),
    R is R1.

gcd(X,0,X).
gcd(X,Y,G) :-
    mod(X,Y,R),
    gcd(Y,R,G1),
    G is G1.

% 4 lists
% even
% s functor
even1(0).
even1(s(s(X))) :- even1(X).

% is
even2(0).
even2(X) :- X > 0,
	    X2 is X-2,
	    even2(X2).

% if term is a list of even numbers
leven([]).
leven([X|Xs]) :-even2(X),
		leven(Xs).

```
