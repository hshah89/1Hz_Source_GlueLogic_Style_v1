# 1Hz Clock Source: RTC Based

In this repo, I go over how to generate a 1Hz clock source through an unusual way.

![Cover Image](/pics/cover.jpg)

## **Hardware Components**

Part No. | Description | Quantity
--- | --- | ---
DS3231M | RTC IC | x1
74HC4020 | 14 bit binary counter | x2
1uF, 0603 | Capacitor | x3
4.7k, 0603 | Resistor | x1

## **Story**

I have been looking for an accurate clock source for another project (that I will be publishing here soon). The more accurate an oscillator or crystal is, the more expensive it becomes. The easiest way to generate a 1Hz clock source is to generate or use a 32.768 kHz source. It's a common frequency available and it cleanly divides down to 1Hz.

During my search for accurate 32.768 kHz TCXOs, I found one from Maxim IC. It was their popular DS32xx family of RTC ICs and they specifically made a TCXO version only. From there, I found these two parts: DS3231 and DS3232M. They are RTC chips but also have a dedicated 32.768 kHz output. Two main differences between them is that the DS3231M runs off +2.3 to +5.5 volts and requires a pullup on the 32.768 kHz output.

Now, obviously, using a dedicated a 32.768 kHz TCXO would be the best way to go, but where is the fun in that? I wanted to see if I could use this RTC chip as a standalone 1Hz source (spoiler alert: you can, but with some caveats).

## **DS3231M / DS3232M**

Both the DS3231M and DS3232M have a dedicated 32.768 kHz output pin. The only difference being that the DS3231M requires an external pull up resistor (4.7k should suffice). From here on out, I will only be referring to the DS3231M.

You're probably wondering why would I go thru all this trouble to use a RTC chip that has an I2C interface just to create 32.768 kHz clock source. The details in the datasheet will help answer this question.

The most important question is what steps are needed to actually use the 32.768 kHz output pin. The answer is, it just needs to be powered on from VCC, not the battery. That's it. Let's take a closer look.

Here is the pin description: