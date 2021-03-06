PruningRadixTrie<br> 
[![MIT License](https://img.shields.io/github/license/wolfgarbe/pruningradixtrie.png)](https://github.com/wolfgarbe/PruningRadixTrie/blob/master/LICENSE)
========
**PruningRadixTrie - a Radix trie on steroids**

The PruningRadixTrie is a novel data structure, derived from a radix trie - but 3 orders of magnitude faster.

A [Radix Trie](https://en.wikipedia.org/wiki/Radix_tree) or Patricia Trie is a space-optimized trie (prefix tree).<br>
A **Pruning Radix trie** is a novel Radix trie algorithm, that allows pruning of the Radix trie and early termination of the lookup.

In many cases, we are not interested in a complete set of all children for a given prefix, but only in the top-k most relevant terms.
Especially for short prefixes, this results in a **massive reduction of lookup time** for the top-10 results.
On the other hand, a complete result set of millions of suggestions wouldn't be helpful at all for autocompletion.<br><br>
The lookup acceleration is achieved by storing in each node the maximum rank of all its children. By comparing this maximum child rank with the lowest rank of the results retrieved so far, we can heavily prune the trie and do early termination of the lookup for non-promising branches with low child ranks.

***

### Application:

The PruningRadixTrie can be used for auto-completion, query completion

### Performance

Pruning  Radix Trie: search top-10 results for prefix 'a' in 6.273.234 terms in  **0.05 ms**<br>
Ordinary Radix Trie: search top-10 results for prefix 'a' in 6.273.234 terms in **37.22 ms**

**The PruningRadixTrie is 700x faster**

While 37 ms for an autocomplete might seem fast enough for a single user, it becomes a completely different story if we have to serve thousands of users in parallel. Then autocomplete lookups in large dictionaries become only feasible when powered by something much faster than an ordinary radix trie.


### Operations: 

**AddTerm:** insert a term into the Pruning Radix Trie.

**GetTopkTermsForPrefix:** retrieve the top-k most relevant terms for a given prefix from the Pruning Radix Trie.

**WriteTermsToFile:** Serialise the Pruning Radix Trie to disk for persistence.

**ReadTermsFromFile:** Deserialise the Pruning Radix Trie from disk for persistence.


### Dictionary

Terms.txt contains 6 million unigrams and bigrams derived from English Wikipedia, with term frequency counts used for ranking
