# ArrayList vs Vectors

Pacotes: java.util.ArrayList e java.util.Vector

Garantem ordem de inserção, além de CRUD sem regras adicionais.

Permite ordenação através de comparators.

Qual é a diferença entre Vector e ArrayList?

[Resposta StackOverflow](https://stackoverflow.com/questions/2986296/what-are-the-differences-between-arraylist-and-vector): "As the documentation says, a Vector and an ArrayList are almost equivalent. The difference is that access to a Vector is synchronized, whereas access to an ArrayList is not. What this means is that only one thread can call methods on a Vector at a time, and there's a slight overhead in acquiring the lock; if you use an ArrayList, this isn't the case. Generally, you'll want to use an ArrayList; in the single-threaded case it's a better choice, and in the multi-threaded case, you get better control over locking. Want to allow concurrent reads? Fine. Want to perform one synchronization for a batch of ten writes? Also fine. It does require a little more care on your end, but it's likely what you want. Also note that if you have an ArrayList, you can use the Collections.synchronizedList function to create a synchronized list, thus getting you the equivalent of a Vector."
