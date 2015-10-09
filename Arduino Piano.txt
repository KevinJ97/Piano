int Pin1 = 2; //Sets Pin#2
int Pin2 = 4;
int Pin3 = 6;
int pinSpeaker = 7; //Sets #7 as speaker output pin
int val = 0;

void setup()
{
    pinMode(pinSpeaker, OUTPUT);
    pinMode(Pin1, INPUT);
    pinMode(Pin2, INPUT);
    pinMode(Pin3, INPUT);
}

char notes[] = { 'c', 'd', 'e', 'f', 'g', 'a', 'b', 'C' };

void playTone(int note, int duration)
{
    for (long i = 0; i < duration * 1000L; i += note * 2)
    {
        digitalWrite(pinSpeaker, HIGH);
        delayMicroseconds(note);
        digitalWrite(pinSpeaker, LOW);
        delayMicroseconds(note);
    }
}

void playNote(char note, int duration)
{
    char names[] = { 'c', 'd', 'e', 'f', 'g', 'a', 'b', 'C' }; //Capital C for next octave.
    int tones[] = { 1915, 1700, 1519, 1432, 1275, 1136, 1014, 956 };

    for (int i = 0; i < 8; i++)
    {
        if (names[i] == note)
        {
            playTone(tones[i], duration);
        }
    }
}


void loop()
{
    if (digitalRead(Pin1) == LOW)
    {
        playNote(notes[0], 300);
    }
    else if (digitalRead(Pin2) == LOW)
    {
        playNote(notes[1], 300);
    }
    else if (digitalRead(Pin3) == LOW)
    {
        playNote(notes[2], 300);
    }
    else
    {
        digitalWrite(pinSpeaker, LOW);
    }
}