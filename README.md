# TPF2-Service-Manager
This is a draft mod that is based on Gregory365's adaptation on the TimeTables mod.
This mod is in its very early design stage.

## Mission & Core Idea
The mod is an attempt to provide a tool to implmenet complicated service patterns (local, limited, express),
on a passanger only, dedicated trunk line.

Instead of looking at movement management as "lines", 
this mod attempt to construct movement management as "sevices".

The reallife services below serves 東京駅 (tokyo station), 
where we can see there are three properties regarding different lines in a service at a point,
direction, terminal station(*), and service pattern.

![image](https://user-images.githubusercontent.com/26424577/219263199-27756fbd-d1fc-48ce-94b0-95e10790e94f.png)

### Direction 

Even if we treat movements as a service instead of a line,
the majority of services is still shaped like a line,
the direction is just the general direction of travel consistentent across multiple service patterns.

### Terminal Station

Lines within one service can have different terminal station in the same direction, 
for example this 主线 支线 (trunk-line, branch-line) pattern used widely in Shanghai:
![image](https://user-images.githubusercontent.com/26424577/219264747-7d819b5b-cf75-42b9-91ee-d5aa17f71df0.png)

A line may also terminate early in the core trunk line, 
this could be used to increase the frequency and capacity of the core segment while keeping the maintaince requirement low.

In the US, this branching and early termination service pattern is often represented as multiple lines interlining with each other.

For example, DC's subway system consists two (three?) sets of branching mainlines,
where the core section is heavily internlined.

![image](https://user-images.githubusercontent.com/26424577/219267535-d7ac1e77-077d-4095-844d-6e87d78919e1.png)

### Service pattern
The service pattern being discussed here regards the stop pattern of the movement. 
A local line is a line where the the train stops at all stations,
an rapid/express line is a line where the train stops at only some stations.
Of coures we can build hierarchy here, 
for example, 
a local line is a line that services all stations,
a rapid line is a line that services non-insiginificant stations, 
a express line is a line that only services major stations,
a limited express line is a line that only services major interchanges.
However, assuming the trunk line has limited infrastructure, 
implementing those patterns may be challenging, 
needing the help of time tables and extra station capacities.

# Implementation goals:
By having control over in-station dwelling time, number of trains, and detecting station throughput we can implement:

Step by step:
1. Assume that each line within the service has their dedicated dual track (no conflict among line), 
thus reducing this mod to a line manager, on top of which, implement branching (or even express/local) service pattern.
2. Support branching line service model on constratined infrastructure (thi will implemnet early terminatation service pattern),
where we guarantee a minimal frequency on the core segment and a minmium frequency on the branching segments with bias.
3. Support local / express service pattern on dual track trunk line,
where we guarantee a minmial frequency on some time point stations for each line and suggest a best case timetable.

# Future ideas
1. Allow mixing of the two service pattern in one service (express service from branch A to core and terminate early)
2. Support local+express+limited express service pattern on three track trunk line.
3. Allow reassignment of train midway in the service if needed to minimize maintaince 
(at terminal / storage station, reassign infrequent express train to local train).
4. Allow even/odd stop station design running on the same trunk line (with bypass line).
