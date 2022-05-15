## Delaying a Checkpoint
There are two types of checkpoints: 
- `(game_save)` 
*which is a regular boring normal forced checkpoint.*

- `(game_save_no_timeout)`
*The much much cooler checkpoint that allows us to delay it indefinitely.*

Halo: Reach handles checkpoints by checking if all the players are 'safe', if they are considered 'safe' the players will be granted a checkpoint.

What the game considers to be 'danger':
- Enemy ai nearby.
- Projectiles nearby.
- Players taking damage.
- Players shooting.
- Players punching.
- Jumping.
- Falling.
- Standing in a return to battlefield/death barrier.
- Standing in a small area.
- Moving too fast. (ie: Flying in a air vehicle or being launched.)
