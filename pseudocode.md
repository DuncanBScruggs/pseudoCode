# Submarine depth control

### Submarines use ballast tanks that fill with water to 


START

    INIT()

    Input desiredDepth(x)

    DISPLAY desiredDepth

    READ depthGauge

    INIT currentDepth(y)

    DISPLAY currentDepth

    IF desiredDepth > currentDepth

        increaseDepth(x,y)

    ELSE IF desiredDepth < currentDepth

        decreaseDepth(x,y)

    ELSE maintain currentDepth

    ENDIF

END

Function increaseDepth

    READ desiredDepth
    READ currentDepth
    READ ballastWaterLevel

    INIT sternDivePlanes  // dive planes angle the submarine

    INCREMENT sternDivePlanes  // increases the angle of the planes to angle the submarine down
        
    CALCULATE newballastWaterLevel = (ballastWaterLevel + intakeWater) //amount of water intake needed to descend to and be bouyant at desired depth

    WHILE (ballastWaterLevel != newballastWaterLevel)
        OPEN ballastWaterVents // allows intake of water
        OPEN ballastAirVents // allows the release air to allow intake of water
        INCREMENT ballastWaterLevel
    ENDWHILE    
    
    WHEN desiredDepth = currentDepth
        DISPLAY currentDepth
        DECREMENT sternDivePlanes
        ENDFUNCTION
    

Function decreaseDepth

    READ desiredDepth
    READ currentDepth
    READ ballastWaterLevel

    INIT sternDivePlanes  // dive planes angle the submarine

    DECREMENT sternDivePlanes  // decreases the angle of the planes to angle the submarine up
        
    CALCULATE newballastWaterLevel = (ballastWaterLevel + compressedAir) //amount of compressed air needed to expell the excess water and be bouyant at desired depth

    WHILE (ballastWaterLevel != newballastWaterLevel)
        OPEN ballastWaterVents // allows expellation of water by compressed air
        ENGAGE compressedAir
        DECREMENT ballastWaterLevel
    ENDWHILE    
    
    WHEN desiredDepth = currentDepth
        DISPLAY currentDepth
        INCREMENT sternDivePlanes
        ENDFUNCTION


Function INIT

    CREATE Submarine
    CREATE HelmsMan
    CREATE DiveControls

END

Must have
    Ability to adjust and maintain depth through use of ballast tanks and dive planes.

Should Have


Could Have
    Way to more finely adjust depth.

Wont Have
    Way to turn the submarine horizontaly.