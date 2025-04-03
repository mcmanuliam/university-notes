#global 

These are the most common relations/equivalences.

---

| **Category**                            | **Law**                       | **Symbolic Representation**                                  | **Explanation**                                                                      |
| --------------------------------------- | ----------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| **Identity Laws**                       | Union with Empty Set          | $$ A \cup \emptyset = A $$                                   | The union of any set with the empty set results in the set itself.                   |
|                                         | Intersection with Universe    | $$ A \cap U = A $$                                           | The intersection of any set with the universal set results in the set itself.        |
| **Domination Laws**                     | Union with Universe           | $$ A \cup U = U $$                                           | The union of any set with the universal set results in the universal set.            |
|                                         | Intersection with Empty Set   | $$ A \cap \emptyset = \emptyset $$                           | The intersection of any set with the empty set results in the empty set.             |
| **Idempotent Laws**                     | Union with Itself             | $$ A \cup A = A $$                                           | The union of any set with itself is just the set.                                    |
|                                         | Intersection with Itself      | $$ A \cap A = A $$                                           | The intersection of any set with itself is just the set.                             |
| **Double Complement Law**               | Double Complement             | $$  \overline{(\overline{A})} = A $$                         | Taking the complement twice returns the original set.                                |
| **Commutative Laws**                    | Union                         | $$ A \cup B = B \cup A $$                                    | The order of sets in a union doesn't matter.                                         |
|                                         | Intersection                  | $$ A \cap B = B \cap A $$                                    | The order of sets in an intersection doesn't matter.                                 |
| **Associative Laws**                    | Union                         | $$ A \cup (B \cup C) = (A \cup B) \cup C $$                  | The grouping of sets in a union doesn't matter.                                      |
|                                         | Intersection                  | $$ A \cap (B \cap C) = (A \cap B) \cap C $$                  | The grouping of sets in an intersection doesn't matter.                              |
| **Distributive Laws**                   | Union over Intersection       | $$ A \cup (B \cap C) = (A \cup B) \cap (A \cup C) $$         | Union distributes over intersection.                                                 |
|                                         | Intersection over Union       | $$ A \cap (B \cup C) = (A \cap B) \cup (A \cap C) $$         | Intersection distributes over union.                                                 |
| **De Morgan's Laws**                    | Complement of Union           | $$ \overline{A \cup B} = \overline{A} \cap \overline{B} \ $$ | The complement of a union is the intersection of the complements.                    |
|                                         | Complement of Intersection    | $$  \overline{A \cap B} = \overline{A} \cup \overline{B} $$  | The complement of an intersection is the union of the complements.                   |
| **Absorption Laws**                     | Absorption of Union           | $$ A \cup (A \cap B) = A $$                                  | Union of a set with its intersection with another set is just the set.               |
|                                         | Absorption of Intersection    | $$ A \cap (A \cup B) = A $$                                  | Intersection of a set with its union with another set is just the set.               |
| **Complement Laws**                     | Union with Complement         | $$ A \cup \overline{A} = U $$                                | The union of a set with its complement is the universal set.                         |
|                                         | Intersection with Complement  | $$ A \cap \overline{A} = \emptyset $$                        | The intersection of a set with its complement is the empty set.                      |
| **Complement Conversion to Difference** | Set Difference and Complement | $$ A \cap \overline{B} = A - B $$                            | Intersection with the complement of another set is equivalent to the set difference. |
