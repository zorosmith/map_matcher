# map_matcher
map_matcher is a ros node which matches a source map to a reference map.

## Example - Using Map Matcher to Localize
- Create a map with gmapping. When done, save ```map.yaml``` and ```map.pgm``` to ```~/maps/``` .
- run gmapping again. It should be publishing a map to the topic ```/map``` (```nav_msgs/OccupancyGrid```)
- While gmapping is running, launch the localizer_example:  
```$roslaunch map_matcher localizer_example.launch```

After successful map matching, both maps should be visible in rviz, and transforms between the two map frames will be published to tf.

![a successful match in rviz](https://github.com/danieldugas/map_matcher/blob/master/map_matcher.png)

## map_matcher node
The map_matcher node by itself exposes two services:
- set_reference_map (map_matcher.srv.SetReferenceMap) 
- match_to_reference (map_matcher.srv.MatchToReference)

set_reference_map: expects a map in the format nav_msgs/OccupancyGrid.
match_to_reference: runs the branch and bound matching algorithm. 
                    expects a map in the format nav_msgs/OccupancyGrid
                    returns the match information (success, pose, angle, score)
                    
Both maps should have similar resolutions for the matching algorithm to succeed.



