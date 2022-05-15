# Revert Reverting 
First appearing in halo 2, revert reverting is a soft-lock prevention mechanic for bad checkpoints where potential revert loops can occur causing the player to be stuck dying infinitely. A revert loop can occur if a someone hits a checkpoint whilst driving recklessly and falls off the map. To prevent this, the game has a fail safe where it checks whether all players are dead within a 7 second time frame. If this check fails after 5 tries, the game will send you back to the previous checkpoint.

> *If a revert revert happens it is interesting to note that the game will not do multiple reverts in a row.*
> *(There has to be a buffer of atleast one checkpoint before the game will allow the machanic to work again.)*