/*read wiki for information about how to make it work*/

let i (integer)

let PT(Point)
let PL(plane)
let C1(circle)
let C2(circle)
let su(surface)
let yy(integer)
let c(Point)
let d(integer)
let p1(Point)
let p2(plane)
let cur(curve)
let DIR(direction)
let g(curve)
let g1(point)
let g2(point)

let f1(curve)
let f2(curve)
let fp(point)
let fp2(point)


let PROF(curve)
let SURF(surface)

set PT = CreateOrModifyDatum("Point", points ,`Relations\Knowledge Pattern.1\Points`, 1)
set PT = pointoncurveRatio(`Geometrical Set.1\Sketch.2` ,`Geometrical Set.1\Point.1` ,0 ,true)

i=1
for i while i <=  lev_count {
	set PT = CreateOrModifyDatum("Point", points ,`Relations\Knowledge Pattern.1\Points`, i+1)
	set PT = pointoncurveRatio(`Geometrical Set.1\Sketch.2` ,`Geometrical Set.1\Point.1` ,i/lev_count ,true) 
	i = i+1
}

i=1
yy=1
for i while i <= `Relations\Knowledge Pattern.1\Points` ->Size()    {
	
	p1= `Relations\Knowledge Pattern.1\Points`->GetItem(i)
	
	set C1 = CreateOrModifyDatum("Circle", circles  ,`Relations\Knowledge Pattern.1\circles` , yy)
	set C1 = circleCtrRadius(p1  , `xy plane`  , inner_d  , 0 , 0deg  , 360deg )
	
	yy=yy+1
	
	set C2 = CreateOrModifyDatum("Circle", circles  ,`Relations\Knowledge Pattern.1\circles` , yy)
	set C2 = circleCtrRadius(p1 , `xy plane` , outer_d ,  0 , 0deg  , 360deg )
	
	i=i+1
	yy=yy+1
	/*Message("y nech")*/
	
	if i <= `Relations\Knowledge Pattern.1\Points` ->Size()
	{
		p1= `Relations\Knowledge Pattern.1\Points`->GetItem(i)
		
		set C2 = CreateOrModifyDatum("Circle", circles  ,`Relations\Knowledge Pattern.1\circles` , yy)
		set C2 = circleCtrRadius(p1  ,`xy plane` ,outer_d ,  1 , 0deg  , 360deg )
		yy=yy+1
		
		set C1 = CreateOrModifyDatum("Circle", circles  ,`Relations\Knowledge Pattern.1\circles` , yy)
		set C1 = circleCtrRadius(p1  ,`xy plane` , inner_d , 1 , 0deg  , 360deg )
		i=i+1
		yy=yy+1
		/*Message("i chet")*/
	}
	else
	{
		Message("end")
		
	}
}
DIR=direction(`yz plane`  ) 
i=1
for i while i <= `Relations\Knowledge Pattern.1\circles` ->Size() {
	cur=`Relations\Knowledge Pattern.1\circles` ->GetItem(i) 
	set c = CreateOrModifyDatum("Point", points_2  , `Relations\Knowledge Pattern.1\point_2`  , i)
	c=extremum(cur,DIR, true, NULL, NULL , NULL , NULL) 
	i=i+1
}

d=1
i=1
for d while d<=  (`Relations\Knowledge Pattern.1\circles` ->Size() -1) {
	g1=`Relations\Knowledge Pattern.1\point_2` ->GetItem(i) 
	g2=`Relations\Knowledge Pattern.1\point_2` ->GetItem(i+1) 
	set g = CreateOrModifyDatum("Curve", spline   , `Relations\Knowledge Pattern.1\spline`   ,i)
	g=line(g1,g2) 
	i=i+1
}

f1=CreateOrModifyDatum("Curve",spline , `Relations\Knowledge Pattern.1\spline`  , 0) 
f1=line(`Relations\Knowledge Pattern.1\Points` ->GetItem(1) , `Relations\Knowledge Pattern.1\point_2` ->GetItem(1)) 

fp=`Relations\Knowledge Pattern.1\Points` ->GetItem(`Relations\Knowledge Pattern.1\Points` ->Size() ) 
fp2=`Relations\Knowledge Pattern.1\point_2` ->GetItem(`Relations\Knowledge Pattern.1\point_2`->Size()  ) 
f2=CreateOrModifyDatum("Curve",spline , `Relations\Knowledge Pattern.1\spline`  , `Relations\Knowledge Pattern.1\spline`->Size() +1 ) 
f2=line(fp  , fp2 )

PROF=CreateOrModifyDatum("curve",`Geometrical Set.1` ,`Relations\Knowledge Pattern.1\prof` ,1) 
PROF=assemble(`Relations\Knowledge Pattern.1\spline` ) 
