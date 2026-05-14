![Hero Banner](.github/assets/banner.png)

Six Stars of Separation is a small experiment that tries to address the "[Six Degrees of Separation](https://en.wikipedia.org/wiki/Six_degrees_of_separation)" hypothesis - that "all people are six or fewer social connections away from each other" - in the context of the GitHub user graph: enter two GitHub usernames, and the app tries to chart a route between them using only public follow and starring relationships.

The idea that motivated the original "Six Degrees" theory was that despite the enormous magnitude of the human population, societies tend to be so intertwined that within only six steps you can connect any two people. Since GitHub is kind of a world unto itself, we thought it might be interesting to extend this idea to the GitHub user graph.

## Try It

Live site: [six-stars.hesreallyhim.com](https://six-stars.hesreallyhim.com/)

No ads, no cross-site user tracking.

## How It Works

You can think of the algorithm as using an undirected graph where the nodes are either users/orgs or repos, and an edge exists just in case User A follows User B, or vice versa (or both), _or_ the node is a repo that users A and B have both starred. (This is just one plausible interpretation of "Six Degrees" amongst many.) It uses a bi-directional Breadth-First Search, however because of the magnitude of the graph, we limit the exploration of each frontier of the BFS to one page of results from the GitHub API, which is at maximum 100.

That means we do not perform an exhaustive BFS, and it's quite possible that (a) if a path is found, it may not be a shortest path; and, (b) if a path is not found, that does not entail that one does not exist. But, after all, it's more like a game than a scientific proof.

The results from the GitHub API from previous searches are stored in a database, which we use as a cache to increase the potential range and accuracy of the algorithm - so, the more people who use it, the more accurate it will become, due to the growing size of the cache. (When the app returns a path that involves a cached edge between two users, we try to validate that the cached data is not stale.)

> [!NOTE]
> None of the data that is collected and stored for the purposes of improving the search capacity, as described above, is linked to the person who is performing the search - you don't even need to be a GitHub user to use the app.

## Feedback

Please use GitHub Issues for:

- weird or surprising routes, including routes that show incorrect data (granted that very, very recently updated data may not be reflected yet)
- usernames that should work but do not
- confusing result states
- accessibility problems
- abundant praise for the maintainer
- ideas for better graph visualization
- just saying how cool it is and how the maintainer is very cool as well

---

This project was authored by @hesreallyhim and OpenAI's Codex. It is not endorsed or affiliated with GitHub.
