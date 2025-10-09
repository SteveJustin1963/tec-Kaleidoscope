```
:A
  `Seed (0-9): ` 
  /K 48 - s !
  s 1 + s !
  66 w !
  26 h !
  w 2 / x !
  h 2 / y !
;

:B
  s 37 * 17 + s !
  s 256 > ( s 256 - s ! )
;

:C
  /i x - u !
  /j y - v !
  u 0 < ( u -1 * u ! )
  v 0 < ( v -1 * v ! )
  u v + d !
;

:D
  B
  d 5 * s + r !
;

:E
  D
  r 32 & 0 = ( 
    d 3 < ( 64 /C ) /E (
    d 6 < ( 111 /C ) /E (
    d 9 < ( 43 /C ) /E (
    d 12 < ( 45 /C ) /E ( 46 /C ) ) ) )
  ) /E (
    d 4 < ( 35 /C ) /E (
    d 8 < ( 42 /C ) /E ( 32 /C ) )
  )
;

:F
  C E
;

:G
  h (
    w ( F )
    /N
  )
;

:H
  A G
  /N `Run H for new!` /N
;

H

```


