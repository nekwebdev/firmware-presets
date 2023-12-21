## NAVL1_PERIOD 

To tune beyond that level you should fly a rectangular mission in AUTO mode and adjust NAVL1_PERIOD down by 1 at a time until the aircraft turns at a rate you are happy with, and does not “wag its tail” in flight.
You can additionally adjust the `NAVL1_DAMPING` and `WP_RADIUS` for further tuning.

Without an airspeed sensor, both the pitch trim and the TRIM_THROTTLE parameter would need to be changed appropriately for the desired mid-stick cruise speed.

Tip

Often planes need 2 or 3 degrees of pitch trim to fly at their optimum cruising speed/throttle rather than at the fuselage/autopilot level pitch, especially small light planes or gliders. This can be done at setup by:

(Preferred) Add the desired degrees nose up(usually) or down to TRIM_PITCH_CD.

Position vehicle with a few degrees nose up or down during the first, Level step of accelerometer calibration to match the cruising attitude.

Position vehicle with a few degrees nose up and use the Calibrate Level button on the Mission Planner page. This adjusts the AHRS_TRIM parameters. AHRS_TRIM parameters can only change the difference between the autopilot’s plane and “level” by 10 degrees maximum. If more is needed, (e.g. the autopilot is mounted slightly downward), then you can use TRIM_PITCH_CD to alter the AOA manually.

Tip

You can examine ATT.Pitch in the logs when at cruise speed in FBWB or CRUISE to determine the average pitch trim required in these modes. Appropriately adjusting TRIM_PITCH_CD to lower this to zero when flying level in these modes.


Set initial parameters - when no airspeed sensor is used¶
Using a GCS and assistant, or flight logs:

Setup the desired cruising speed and throttle in FBWA. This can be adjusted using the TRIM_PITCH_CD parameter to get level flight at the desired throttle level. If cruising speed is too great, lower throttle and increase TRIM_PITCH_CD until altitude is constant, or vice-a-versa. Set the TRIM_THROTTLE to that throttle value.

In FBWA, do a full throttle full back stick climb (you can also lower this throttle value with THR_MAX if full throttle seems excessive). Set LIM_PITCH_MAX such that you maintain close to the cruising speed, or at least not less than a safe flying speed. Note the steady state climb rate, and set TECS_CLMB_MAX to 80% of that value for margin at low battery. You can set lower pilot demanded climb rates with FBWB_CLIMB_RATE, but you want TECS to have the maximum capability of you aircraft for sudden altitude demand changes, like switching to RTL, to maximize its climbing ability in order to get out of bad situations.

Set TECS_PITCH_MAX to LIM_PITCH_MAX.

Now idle the throttle while sticks are centered and establish the descent rate. Set TECS_SINK_MIN to that rate.

Using idle throttle, push full down elevator and establish this new sink rate. If the aircraft overspeeds, set the LIM_PITCH_MIN to a higher value. Set TECS_SINK_MAX to that maximum sink rate.

Note

ARSPD_FBW_MIN, TRIM_ARSPD_CM, and ARSPD_FBW_MAX are not used when no airspeed sensor is present (unless TECS_SYNAIRSPEED is enabled, which is usually not recommended since the synthetic airspeed estimate can be very wrong on occasion. However, ARSPD_FBW_MIN and ARSPD_FBW_MAX should be set to the normal minimum and maximum flying speeds in order for AUTOTUNE and STALL PREVENTION features to work properly.


PTCH2SRV_RLL: This parameter controls how much elevator to add in turns to keep the nose level. Many aircraft require a small change to this parameter from the default of 1.0. To see if you need to tune this value you should hold a tight circle in FBWA mode by holding the aileron stick hard over while not giving any elevator input. If the plane gains altitude then you should lower PTCH2SRV_RLL by a small amount (try lowering to 0.95 initially). If the plane loses altitude while circling then try raising PTCH2SRV_RLL by a small amount (try 1.05 initially). If you need to go above 1.3 or below 0.8 then there is probably a problem with your setup (such as incorrect center of gravity, poor thrust line, poor airspeed calibration, too soft a tune on the pitch loop, or bad compass errors). You should try and fix the setup.


Setting up KFF_RDDRMIX for Coordinated Turns¶
Rapidly roll the model from maximum bank angle in one direction to maximum bank angle in the opposite direction in FBWA. Do this several times going in each direction and observe the yawing motion of the model. If as the wings pass through level the nose is yawed in the opposite direction to the roll (for example when rolling from left to right bank, the nose points left) then increase the value of KFF_RDDRMIX gain until the yaw goes away. Do not use a value larger than 1. Conversely, lower it if the nose is yawing into the turn. The default value for KFF_RDDRMIX is usually close



# Autotune

## AUTOTUNE_LEVEL

Start with 6, try 5/7/8 to see what works best for the purpose

## TRIM_PITCH_CD

Calibrate level with thrust angle, most likely increase `TRIM_PITCH_CD`.
Setup the desired cruising speed and throttle in **FBWA**. This can be adjusted using the `TRIM_PITCH_CD` parameter to get level flight at the desired throttle level. If cruising speed is too great, lower throttle and increase `TRIM_PITCH_CD` until altitude is constant, or vice-a-versa. Set the `TRIM_THROTTLE` to that throttle value.
*NOTE THE AIRSPEED at that cruise speed.*
Fly in **CRUISE**, check logs for `ATT.Pitch` and ensure it is zero.

## PTCH2SRV_RLL

In **FBWA** hard constant turn, if loose alt increase by 0.05

## WP_LOITER_RAD

Find a radius where it is roughly over half of `LIM_ROLL_CD`?

## TECS_CLMB_MAX / LIM_PITCH_MAX

In **FBWA** and ideally at low battery (3.4/3.5V), do a full throttle full back stick climb (you can also lower this throttle value with THR_MAX if full throttle seems excessive). Set `LIM_PITCH_MAX` such that you maintain close to the cruising speed you noted. Note the steady state climb rate, and set `TECS_CLMB_MAX` to 80% of that value for margin if not at low battery. You can set lower pilot demanded climb rates with `FBWB_CLIMB_RATE`, but you want TECS to have the maximum capability of you aircraft for sudden altitude demand changes, like switching to RTL, to maximize its climbing ability in order to get out of bad situations.




Plan square mission:
Observe the behaviour of the plane in the turns. If it turns too slowly then reduce NAVL1_PERIOD by 5. If it is “weaving” after a turn then increase NAVL1_PERIOD by 1 or 2

If you are tuning for maximum performance, once you have completed the tuning of NAVL1_PERIOD you can increment NAVL1_PERIOD by 1 and then modify NAVL1_DAMPING in steps of 0.05 to get the response you want. Do not decrease NAVL1_DAMPING too much - it is unlikely you will need a value below 0.6.






Set TECS_PITCH_MAX to LIM_PITCH_MAX.

Now idle the throttle while sticks are centered and establish the descent rate. Set TECS_SINK_MIN to that rate.

Using idle throttle, push full down elevator and establish this new sink rate. If the aircraft overspeeds, set the LIM_PITCH_MIN to a higher value. Set TECS_SINK_MAX to that maximum sink rate.



USING LOGS:

setup fbwb, fly a bit around for logs to adjust TRIM_PITCH_CD

Set LIM_PITCH_MIN by cutting throttle full pitch down and checking speeds to not go too fast.

wait for 3.4V:
FBWA max pitch for climb, throttle at THR_MAX.
If airspeed drops under speed when going TRIM_THROTTLE (35%) reduce LIM_PITCH_MAX
once set at low bat again do a max thr max climb and note climb rate. Set TECS_CLMB_MAX

Cut throttle and glide down, note sink rate. Set TECS_SINK_MIN
TECS_SINK_MAX (in metres/second). If this value is too large, the aircraft can over-speed on descent. This should be set to a value that can be achieved without exceeding the lower pitch angle limit and without exceeding ARSPD_FBW_MAX.
