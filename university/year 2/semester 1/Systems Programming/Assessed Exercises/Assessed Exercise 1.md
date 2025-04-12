#sp
# Search
I'm handling this one asynchronously it's relatively simple, check if the root is `NULL` if it is it'll return `NULL`, else it'll check if found then return a pointer to the node, if neither of these it'll recursively call itself picking left and right until the end of the tree or the value is found.

# Generation

## `node_t* createTree(firstElem)`
`createTree` will take in a root element, allocate a space in memory to it as a node, if failed to allocate return `NULL` if successful it'll create the root node and return it.

## `void destroyTree(node)`
Another recursive one, this one is the simplest of the lot, first I check if the root passed in is `NULL`, if so it'll just return out, if it isn't `NULL` it'll call itself for the left and right node, then it'll free the current node.

# Maintenance
## `void insert(node, elem)`
Here's another recursive one, this time it does another traversal of the tree where left is less than new element and right is larger, it will keep on traversing and if a node is null it will fill that place.

## `void delete(root, elem)`
First off we will find the node to delete and save the parent, this makes what I do later a lot easier. Although the next bit is a bit annoying depending on what situation we are deleting we use different blocks.
## Case 1: Leaf Node
This essentially is just a case of freeing the current node and setting the parent to point towards `NULL`.
## Case 2: Two Children
This ones the most complicated one, first we save the successor from the right side, then we find the lowest value on that right side. Once we've got that we set the current value to the successor and free it.
## Case 3: One Child
We will determine the child depending on which ones `NULL`,  then using that we will set the `current->value` to the child value and the current pointer to the child to `NULL` once we've done that we then free the child.

# Memory Management

The functions are all memory safe through allocating and deallocating memory when needed. 

- Memory for nodes is allocated in `insert`. If allocation fails, the functions return `NULL` to avoid bad accessing.

- Nodes are recursively frees in `destroyTree` ensuring nothing is left allocated.

- After freeing a node, I update pointers to not accessing invalid memory.