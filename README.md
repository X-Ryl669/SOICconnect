# SOICconnect
A production tool using off the shelf components like [this one](https://www.amazon.fr/ARCELI-Programmation-Circuit-EEPROM-adaptateurs/dp/B07BP7S3HD/ref=sr_1_1).
The main idea comes from Simon Merrett and his [SOICbite](https://github.com/SimonMerrett/SOICbite)

His solution is very nice, compact and simple for development work.
In this repository, you'll find a different solution trying to solve a different goal: producing a PCB board in large quantity.

The main idea here is to buy the low cost SOIC clip as shown above, 3D print some model you'll find here, glue it on the clip and start programming your boards (either yourself or by any worker).
The part will look like this:
![Part on clip](pic/SOICFang.jpg?raw=true "SOICConnect")

In order to acheive this, the solution must provide the following features:

1. Prevent pluging the clip badly (either in wrong direction or with pins shifted)
2. Align the board correctly while pluging (or respectively, align the clip correctly while pluging)
3. Have a visual clue about the current alignment
4. Detect connection

## Connection safety
The connection safety is provided by these shapes:
![Fang and border](pic/FangAndBorders.jpg?raw=true "Fang and borders")
**In green**: The sides to push the PCB board onto (so the distance from the PCB edge and the connection is fixed)

**In red**: The assymetric fang to fit into the PCB's footprint hole. This ensures the lateral fitting so the clip does not connect to an unexpected pin

**In blue**: A groove that's visible from the bottom of the part when pluging the system so it's possible to align the clip even without seeing the fang.

The clip mates with this footprint:

![Footprint](pic/SOICClipFootprint.jpg?raw=true "Footprint")

The dimensions here are simple: 
The pad must be 3mm from PCB edge and the hole in the PCB is a round hole of 0.8mm x 2mm located 5.3mm from the edge and centered between the first 1.27mm picthed 2 pads.

In 3D:

**Bottom**:

![Bottom](pic/SOICClipExample.jpg?raw=true "Bottom")

You'll align the groove with the white line.

**Top**:

![Top](pic/SOICClipExample2.jpg?raw=true "Top")

## Some notes
The element that's glued on the clip should be on a single side (typically the bottom side). 
You can place components on the opposite side starting from 5.5mm around the pads (that's the width of the clip), they'll not disturb the clip.
You need to cut the clip's internal plastic (like for SOICbite) so it can pinch your PCB board (I'm doing it with a cutter, the plastic is soft enough to do it gradually easily).

This system is made for PCB down to 0.8mm thick (and up to 2mm it's reasonable).

The STL files are made for a tight fit on the clip (you need to force a bit to fit the part on the clip). 

You might need to resize them by +/- 2% or so depending on your printer resolution.
The part is small enough to print in 10mn and it does not require any support so cleaning is very easy. 

Compared to SOICbite, this solution takes a bit more space on the PCB but still much less than a TagConnect solution. I think that's a correct tradeoff for the safety it gives.

## Compared to other (existing) solutions

| Solution | Price | Usability | Requirement |
|----------|-------|-----------|-------------|
| **TagConnect** | ~$40 | Average. This requires manual work to lock and unlock legs, contacts are not that great and you need free space to operate the connection above your board | The footprint is simple but the cable is not. You must choose between 6 or 10 pins connector |
| **Pogo pins** | High | Probably the best solution if you can afford making a jig to hold the pins for each model of the PCB | You need a jig that will be costly to build and test |
| **SOICbite** | Low $10 | Correct for experienced worker | You must cut the power on the clip before connecting it else any misalignement error might burn your PCB (and they are possible since there is no tactile feedback on the correct alignement) and re-enable it afterward. It's too error prone to be done in a production line, since an error cost you a complete board |
| **SOICConnect** | Low $10 | Good for any worker | Can be used while keeping the clip powered since the fang prevent connecting the wrong pins, and there is a tactile feedback when touching the board edge and when the fang enters the PCB hole, so it's possible to chain board programming faster |
| **JST connector** | Highest | Low | Each board will need a female connector that'll probably used only once. Not convenient for chain programming since unplugging the connector is a bit dangerous if done badly. Also, it takes a lot of space on PCB. |
