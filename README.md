/*look at the pictures to see what it does*/

Just download leg_0.CATPart

OR

if you need to make file from scratch, you have to create:

    parameters:
        leg_length
        lev_count
        inner_d
        outer_d
    lists in knowledge pattern:
        Points
        circles
        point_2
        spline
        prof
    geometrical sets:
        Geometrical Set.1 (usually is created by default)
        points
        circles
        points_2
        spline
    geometry:
        sketch named Sketch.2 lenged by parameter leg_length
        point named Point.1 on this skecth with ratio 0

and copy script.txt to knowledge pattern editor window

You can change parameters to change its length, levels count, inner diameter or outer diameter. 

When it's done, you get spline in Geometrical Set.1 and you can just Shaft  it using Sketch.2 as an axis

My very first code but maybe it will be helpful for someone
