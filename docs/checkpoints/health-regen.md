# Health Regeneration
In extremely specific instances it is possible for Halo: Reach to grant the player a checkpoint for health regeneration. There is a dormant script `f_global_health_saves` in Halo: Reach's campaign, but it goes for the most part unused because most missions don't trigger `(wake f_global_health_saves)` in the mission script startup.

Missions that use `f_global_health_saves`:
- Winter Contingency 
- Tip of The Spear

Both missions use different implementations of `f_global_health_saves`. 

*Winter Contingency has a check in the script start-up to see if the game is in `Solo` or `Co-op`. If a player is in a `Co-op` game `f_global_health_saves` will be left dormant, unable to be used for checkpoint exploits.*

`(if (not (game_is_cooperative)) (wake f_global_health_saves))`


*Tip of The Spear does not differentiate and proceeds to run the wake script along with all the other crucial startup scripts.*

`(wake f_global_health_saves)`

> *With the differences of the mission specific initializations established, how does `f_global_health_saves` actually work?*

The game checks to see if the health of `player0` drops below 100% `object_get_health player0 < [1.0]`. Once `player0`'s health reaches ~66% they can no longer regenerate health without assistance. 

If the player restores their health back to 100% within 7 seconds of the initial regeneration `(= (object_get_health player0) 1.0)`, the game will grant a checkpoint if the player is not considered to be in 'danger'.
```css
(script dormant void f_global_health_saves
    (sleep_until (> (player_count) 0))
    (sleep_until 
        (begin
            (sleep_until (< (object_get_health player0) 1.0))
            (sleep (* 30.0 7.0))
            (if (< (object_get_health player0) 1.0) 
                (begin
                    (sleep_until (= (object_get_health player0) 1.0))
                    (print "global health: health pack aquired")
                    (game_save)
                ) (print "global health: re-gen"))
            false
        )
    )
)
```
*From looking at the script above, it is clear that the developers intended for a checkpoint to drop after picking up a Health Pack, but the `f_global_health_saves` script does not actually check how the player gains the health back. `Player0` can use various methods for health regeneration such as, sitting in a dropshield, hitting loadzones that alter health, quickly dying then staying safe after a respawn, and of course using the intended health pack.*