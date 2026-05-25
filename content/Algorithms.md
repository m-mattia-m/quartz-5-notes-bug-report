---
publish: true
created: 2026-01-29T21:35:21.000+01:00
modified: 2026-03-10T21:57:39.922+01:00
tags:
  - Tech/Algorithms
---

# Binary Search

A search algorithm that works on a **sorted** array (alphabetically or numerically). It compares the value in the middle of the array with the value we are searching for.

If the desired value is smaller than the middle element, we can discard the upper ~50% of the array. If it is larger, we discard the lower ~50%. We repeat this process until we find the desired value.

## Example

Array: 1, 2, 3, 4, 5, 6, 7, 8, 9
Desired value: 8

1. Middle: 5 → 8 > 5
   - New search range → 6, 7, 8, 9
2. Middle: 7 → 8 > 7
   - New search range → 8, 9
3. Middle: 8 → 8 = 8 → **found**

→ It requires 3 iterations to find the value.

Compared to a linear search, we would need up to 8 comparisons in the worst case.

### Drawback

If the array is not sorted — or we cannot guarantee that it is — sorting it first might take longer than simply using another search algorithm.

## When shouldn't you a Binary search

Eine Binary-search ist eine effiziente Möglichkeit, um in einem sortierten Array nach einem bestimmten Element zu suchen, indem man das Array in der Mitte teilt und dann das gesuchte Element in einem der beiden Teilarrays weitersucht. Dies wird wiederholt, bis das gesuchte Element gefunden wurde oder bis das Array leer ist.

Eine Binary-search ist in der Regel die effizienteste Möglichkeit, um in einem sortierten Array nach einem bestimmten Element zu suchen, da sie nur O(log n) Durchläufe des Arrays erfordert, wobei n die Anzahl der Elemente im Array ist.

Wenn Sie jedoch in einem unsortierten Array nach einem bestimmten Element suchen müssen, gibt es möglicherweise effizientere Möglichkeiten als eine Binary-search. Zum Beispiel könnten Sie eine Hash-Tabelle verwenden, um Elemente in O(1)-Zeit zu suchen, oder einen anderen Suchalgorithmus wie die lineare Suche, der das Array sequentiell durchläuft, um das gesuchte Element zu finden. Welche Methode am besten geeignet ist, hängt von den spezifischen Anforderungen und Einschränkungen Ihres Problems ab.

# Map Search / Hashmap

To minimize the runtime complexity _==(DE: Laufzeitkomplexität)==_ use instead of two loops in each other the map. → instead of `m*n` → `m+n`

Use instead of:

```Go
// time obj*as 
// -> e.g. obj.length = 10 | as.length = 9 -> 10*9 = 90
for _, obj := range objects {
	for _, a := range as {
		if obj.id == a.id {
			// do something
		}
	}
}
```

Use this:

```Go
// time as + obj * (map-search-duration) -> very fast (there is nothing faster)
// -> e.g. obj.length = 10 | as.length = 9 -> 9 + 10 * 1 = 19

// if the map-key is a string makes no difference to int
aMap := map[int]interface{} // or use directly the right struct
for _, a := range as {
	aMap[a.id] = a
}

for _, obj := range objects {
	if _, found := aMap[obj.id]; found{
		// do something
	}
}
```

# HNSW – Hierarchical Navigable Small Worlds

- [Hierarchical Navigable Small Worlds (HNSW)](https://www.pinecone.io/learn/series/faiss/hnsw/)
- [Github.com – Buildt-AI/buildt-ssdb](https://github.com/Buildt-AI/buildt-ssdb)

# RANSAC – RANdom SAmple Consensus

- [What is RANSAC?](https://ch.mathworks.com/de/discovery/ransac.html)

# LRU (Least Recently Used) Cache

Would a kind of intelligent cache system make sense that considers the following points?

- Separate cache per form (Source API object), stored in the database
- The cache has a kind of scoring mechanism: forms that are currently accessed more frequently are cached for a longer time
- When a request is sent to my API, the Source API is called in the background on a separate thread and then stored asynchronously in my database. This request might still receive an “outdated” version, but the next request will already be up to date

---

# Examples

- Shazam: [How on Earth Does Shazam Recognize Songs](https://youtu.be/ev0Ay1m4MWs?si=mcTQbx5vx6HX59Sc)
