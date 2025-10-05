 
![image](https://github.com/user-attachments/assets/1d9129f1-e215-4216-bccb-49af61c1bdaf)





 
# MINT Kaleidoscope Generator

![Kaleidoscope Pattern](https://github.com/user-attachments/assets/1d9129f1-e215-4216-bccb-49af61c1bdaf)

```
There once was a scope, quite profound,  
That twisted the stars all around.  
Through mirrors it spun,  
Making galaxies run,  
In patterns so wild and unbound!
```

---

## Table of Contents
- [Conceptual Overview](#conceptual-overview)
- [Key Principles](#key-principles)
- [Functional Breakdown](#functional-breakdown)
- [The Working MINT Implementation](#the-working-mint-implementation)
- [How to Run](#how-to-run)
- [How to Customize](#how-to-customize)
- [Unique Characteristics](#unique-characteristics)
- [Limitations](#limitations)

---

## Conceptual Overview

A kaleidoscope is an optical instrument that creates symmetrical patterns through reflection and rotation. Our MINT implementation simulates this by creating a digital, ASCII-based kaleidoscope that generates unique mandala-like patterns.

Each run produces a **completely different symmetrical design** based on a user-provided seed value, mimicking the experience of turning a physical kaleidoscope.

---

## Key Principles

### 1. Symmetry Creation
- The program calculates distance and angular position for every point on the grid
- It creates reflections across multiple axes
- These reflections create symmetrical patterns, mimicking a physical kaleidoscope

### 2. Randomized Variation
- A pseudo-random number generator creates variation
- Different seed values produce different patterns
- The random element is balanced with strict symmetry rules

### 3. Distance-Based Rendering
- Characters are chosen based on distance from center
- Creates concentric ring patterns
- Angular sectors add radial variation

---

## Functional Breakdown

### 1. Initialization (Function A)
- Accept a single-digit seed (0-9) from user
- Set up grid dimensions (60×24)
- Calculate center point coordinates
- Display confirmation message

### 2. Pseudo-Random Generator (Function B)
- Simple Linear Congruential Generator (LCG)
- Formula: `s = (s × 13 + 7) mod 100`
- Provides variation while maintaining reproducibility with same seed

### 3. Distance Calculation (Function C)
- For each point (i,j), calculate squared distance from center
- Uses Pythagorean theorem: `d = (i-x)² + (j-y)²`
- Creates concentric circular zones

### 4. Symmetry Analysis (Function D)
- Calculate absolute differences from center on both axes
- Used for angular sector determination
- Ensures perfect 4-way symmetry

### 5. Pattern Selection (Function E)
- Combine distance (rings) and angle (sectors)
- Use modulo operations to create repeating patterns
- Select from 11 different ASCII characters
- Nested conditionals create priority-based character selection

### 6. Grid Rendering (Function F)
- Double loop over all grid positions
- For each position, call pattern selector
- Print newline at end of each row
- Creates the final visible output

### 7. Main Program (Function G)
- Orchestrates all functions in sequence
- Warms up random generator with multiple calls
- Displays final pattern
- Prompts user to run again

---

## The Working MINT Implementation

```mint
:A
  `Enter seed (0-9): ` 
  /K
  48 - s !
  60 w !
  24 h !
  w 2 / x !
  h 2 / y !
  `Generating...` /N /N
;

:B
  s 13 * 7 + 100 /mod s !
;

:C
  /i x - " * a !
  /j y - " * b !
  a b + d !
;

:D
  /i x - /abs e !
  /j y - /abs f !
;

:E
  C D
  d /sqrt /floor 5 /mod h !
  e f + s + 6 /mod j !
  h j + k !
  k 0 = (42 /C) /E (
  k 1 = (43 /C) /E (
  k 2 = (35 /C) /E (
  k 3 = (64 /C) /E (
  k 4 = (111 /C) /E (
  k 5 = (79 /C) /E (
  k 6 = (126 /C) /E (
  k 7 = (45 /C) /E (
  k 8 = (61 /C) /E (
  k 9 = (58 /C) /E (
  k 10 = (46 /C) /E (
  32 /C ) ) ) ) ) ) ) ) ) )
;

:F
  0 j !
  h (
    0 i !
    w (
      E
      i 1 + i !
    )
    /N
    j 1 + j !
  )
;

:G
  A
  B B B
  F
  /N /N `Run G again!` /N
;

G
```

---

## How to Run

### Starting the Program

1. Load MINT-Octave interpreter:
   ```octave
   mint_octave_9()
   ```

2. Choose debug mode (recommend 'n' for cleaner output):
   ```
   Enable debug mode? (y/n): n
   ```

3. Paste the entire kaleidoscope code into the REPL

4. When prompted, enter a single digit (0-9):
   ```
   Enter seed (0-9): 7
   ```

5. Watch your unique kaleidoscope pattern render!

6. To generate a new pattern, type `G` and enter a different seed

### Example Session
```
> G
Enter seed (0-9): 3
Generating...

              oo===oo==oo===oo              
            oo===oo====oo===oo==            
          oo===oo======oo===oo====          
        ==oo==oo========oo==oo====oo        
       ===oo=oo==========oo=oo=====oo       
      ====oo=o============o=oo======o       
     =====oooo==============oooo=====o      
    ======ooo================ooo======      
    ======oo==================oo======      
   =======o====================o=======     
   ======o======================o======     
   =====o========================o=====     
   =====o========================o=====     
   ======o======================o======     
   =======o====================o=======     
    ======oo==================oo======      
    ======ooo================ooo======      
     =====oooo==============oooo=====o      
      ====oo=o============o=oo======o       
       ===oo=oo==========oo=oo=====oo       
        ==oo==oo========oo==oo====oo        
          oo===oo======oo===oo====          
            oo===oo====oo===oo==            
              oo===oo==oo===oo              

Run G again!
```

---

## How to Customize

### Change Grid Size
In function `:A`, modify width and height:
```mint
:A
  `Enter seed (0-9): ` 
  /K
  48 - s !
  80 w !    // Make it wider (was 60)
  30 h !    // Make it taller (was 24)
  w 2 / x !
  h 2 / y !
  `Generating...` /N /N
;
```

### Change Characters
In function `:E`, replace the ASCII codes:

| Current Code | Character | Change To | New Character |
|--------------|-----------|-----------|---------------|
| 42 | `*` | 35 | `#` |
| 43 | `+` | 88 | `X` |
| 64 | `@` | 37 | `%` |
| 111 | `o` | 48 | `0` |
| 79 | `O` | 56 | `8` |
| 126 | `~` | 94 | `^` |
| 45 | `-` | 95 | `_` |
| 61 | `=` | 124 | `|` |

Example modification:
```mint
k 0 = (35 /C) /E (    // Change * to #
k 1 = (88 /C) /E (    // Change + to X
```

### Adjust Ring Count
In function `:E`, change the modulo value for rings:
```mint
d /sqrt /floor 8 /mod h !    // More rings (was 5)
```

### Adjust Sector Count
In function `:E`, change the modulo value for angular sectors:
```mint
e f + s + 12 /mod j !    // More sectors (was 6)
```

### Different Random Algorithm
In function `:B`, modify the LCG constants:
```mint
:B
  s 17 * 23 + 100 /mod s !    // Different multiplier & increment
;
```

---

## Unique Characteristics of the MINT Implementation

### Stack-Based Programming
- All operations manipulate a data stack
- No temporary variables except the 26 named registers (a-z)
- Demonstrates how complex visual patterns can emerge from simple stack operations

### Memory Constraints
- Operates within strict memory limitations
- Original MINT had only 2K RAM
- This Octave version relaxes some constraints but maintains the spirit

### Single-Character Operations
- Each operation is typically 1-2 characters
- Functions limited to single letters (A-Z)
- Variables limited to single letters (a-z)
- Extremely compact code representation

### Real-Time Computation
- No pre-computed lookup tables
- Every pixel calculated on-the-fly
- Distance and symmetry computed for each position

### Deterministic Randomness
- Same seed always produces same pattern
- Allows reproducibility and sharing of specific designs
- Pseudo-random generator uses only 64-bit floating point math

---

## Limitations

### Fixed Grid
- Grid size set at initialization
- Cannot dynamically resize during execution
- Larger grids slow down rendering proportionally

### ASCII Only
- No color support
- Limited to printable ASCII characters
- No grayscale or anti-aliasing

### Simple Symmetry
- 4-way symmetry only (not 6-way, 8-way, etc.)
- No rotation beyond 90-degree reflections
- No fractal or recursive patterns

### Integer Arithmetic Constraints
- Uses floating-point but optimized for integer operations
- Modulo operations critical for pattern generation
- Limited precision can affect large distance calculations

### No Animation
- Generates static patterns only
- Would need external loop for animation frames
- No smooth transitions between patterns

---

## Example Patterns by Seed

- **Seed 0**: Dense circular mandala
- **Seed 1**: Sparse starburst  
- **Seed 2**: Concentric rings
- **Seed 3**: Diamond lattice
- **Seed 4**: Diagonal waves
- **Seed 5**: Radial spokes
- **Seed 6**: Checkered symmetry
- **Seed 7**: Snowflake pattern
- **Seed 8**: Cross formation
- **Seed 9**: Spiral approximation

Try them all to find your favorite!

---

## Technical Implementation Notes

### Variables Used
- `s` - Random seed and state
- `w` - Grid width
- `h` - Grid height  
- `x` - Center X coordinate
- `y` - Center Y coordinate
- `a` - (i-x)² temporary
- `b` - (j-y)² temporary
- `d` - Distance squared
- `e` - |i-x| absolute horizontal distance
- `f` - |j-y| absolute vertical distance
- `i` - Current column (also uses `/i` for loop counter)
- `j` - Current row (also uses `/j` for loop counter)
- `h` - Ring number (0-4)
- `j` - Sector number (0-5) [reused]
- `k` - Final pattern selector (0-10)

### Functions Used
- `:A` - Initialize
- `:B` - Random number generator
- `:C` - Distance calculator
- `:D` - Symmetry analyzer
- `:E` - Pattern selector
- `:F` - Grid renderer
- `:G` - Main program

---

## The Beauty of Constrained Computing

This implementation demonstrates how **complex, aesthetically pleasing patterns** can emerge from:
- Minimal code (less than 50 lines)
- Simple mathematical operations
- Stack-based computation
- Constrained resources

It's a testament to creative programming in resource-limited environments—the kind of challenge that defined early computing and continues to inspire programmers today.

---

**Created for MINT-Octave v2.5**  
**Date: 2025-10-05**

*Try different seeds. Share your favorites. Modify the code. Make it yours!*
