# Mistakes to Review

### recursion

- forgot that I needed a return statement on the recursive call in python

### simple linked list impl in python

- I remembered the general pattern of using a node class with next, I used data class but forgot I needed an import and was unsure about using the 'object' type for it
- I caught myself tryign to just manipulate the private 'head' member. I also forgot to set it on self and have self as the implicit parameter to all member functions of the class. I remmembered and used a temp variable so that I wasn't modifying the head reference 4every time. this was a good move
- there were a few false starts with syntax but for the most part worked my way through the problem without getting really stuck. not sure if it is the most efficient but it helped me remember how often we have to linearly search the list in order to insert items.
