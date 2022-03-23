# Muziek of niet

![Drie rijen met muzieknoten.](./images/puzzel-1.png)

Het lijkt alsof bij deze puzzel een muziekstuk uitgeschreven staat, maar hiermee kan de code niet worden gekraakt.
In werkelijkheid is dit een [bacon](https://nl.wikipedia.org/wiki/Baconalfabet) code, waarbij je moet kijken naar de
verandering in toonhoogte om te weten of je een _a_ of _b_ moet noteren.  Hoe weet je welke letter de eerste noot moet
hebben?  We nemen gewoon aan dat deze een _a_ is.  De uiteindelijke volgorde van _a_'s en _b_'s wordt:

```txt
ababb aaaaa abbaa ababb aabaa baaba aaaab
abbaa aabaa abaab aabaa abbaa aabbb abbab
aabaa aaaba
```

Als we dit terugcijferen, krijgen we `manmetbnekenhoec`.  Dit lijkt misschien nergens op, maar als we er een paar
spaties bij zetten wordt het iets meer Nederlands: `man met bnek en hoec`.  De `bnek` en `hoec` lijken nog steeds geen
woorden, maar als je de letters na de `n` en `c` neemt, de `o` en `d`, dan klopt de zin wel: `man met boek en hoed`.
Dit is de oplossing die bij de eerste puzzel hoort.

Marbli Music heeft een korte orkest versie van dit muziekstuk gemaakt: <https://youtu.be/OcHm5J1bIzc>
