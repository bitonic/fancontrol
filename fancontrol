#!/usr/bin/tclsh

# Stupid fan control script that simply blasts the fans when the
# temperature reaches a certain level.

# 2 minutes
set interval 12000

proc gettemp {} {
    set tempsens "/proc/acpi/ibm/thermal"
    return [lindex [split [exec cat $tempsens]] 1]
}

proc controlfan {temp} {
    set threshold 10
    set fansens "/proc/acpi/ibm/fan"

    if {$temp < $threshold} {
        exec echo level auto > $fansens
    } else {
        exec echo level full-speed > $fansens
    }
}

while {1} {
    controlfan [gettemp]

    after $interval
}