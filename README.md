# Cache Behavior Analysis

This project contains a series of C programs designed to analyze and demonstrate different cache behavior patterns in computer systems. The programs explore various memory access patterns and their impact on cache performance.

## Programs Overview

### 1. cache1D.c
**Purpose**: Demonstrates sequential memory access pattern in a 1D array.

**Key Characteristics**:
- Creates a large 1D array of 100,000 integers
- Accesses elements sequentially from beginning to end
- Represents optimal cache behavior with spatial locality

**Expected Cache Performance**: Excellent - Sequential access patterns maximize cache line utilization and minimize cache misses.

### 2. cache2Drows.c
**Purpose**: Demonstrates row-major order access in a 2D array.

**Key Characteristics**:
- Creates a 3000×500 2D array (1,500,000 elements total)
- Accesses elements row by row (outer loop rows, inner loop columns)
- Follows the natural memory layout of C arrays (row-major order)

**Expected Cache Performance**: Excellent - Accesses memory in contiguous blocks, maximizing spatial locality and cache efficiency.

### 3. cache2Dcols.c
**Purpose**: Demonstrates column-major order access in a 2D array.

**Key Characteristics**:
- Uses the same 3000×500 2D array as cache2Drows.c
- Accesses elements column by column (outer loop columns, inner loop rows)
- Violates the natural row-major memory layout

**Expected Cache Performance**: Poor - Causes frequent cache misses as each access jumps across memory regions, breaking spatial locality.

### 4. cache2Dclash.c
**Purpose**: Demonstrates cache conflict misses through strategic memory access patterns.

**Key Characteristics**:
- Creates a 128×8 2D array
- Uses a specific access pattern: processes every 64th row repeatedly
- Designed to cause cache line conflicts in typical cache architectures

**Expected Cache Performance**: Poor - Intentional pattern causes cache conflicts and thrashing due to limited cache associativity.

## Usage

### Compilation
```bash
gcc -o cache1D cache1D.c
gcc -o cache2Drows cache2Drows.c
gcc -o cache2Dcols cache2Dcols.c
gcc -o cache2Dclash cache2Dclash.c
```

### Running the Programs
```bash
./cache1D
./cache2Drows
./cache2Dcols
./cache2Dclash
```

## Performance Analysis

To measure cache performance, use profiling tools such as:

- **perf** (Linux): `perf stat ./program_name`
- **Valgrind with Cachegrind**: `valgrind --tool=cachegrind ./program_name`
- **Intel VTune** or **AMD uProf** for detailed cache analysis

## Key Cache Concepts Demonstrated

1. **Spatial Locality**: cache1D.c and cache2Drows.c show optimal spatial locality
2. **Cache Line Utilization**: Sequential access vs. strided access patterns
3. **Cache Conflicts**: cache2Dclash.c demonstrates associativity limitations
4. **Memory Layout Awareness**: Importance of understanding row-major vs column-major ordering

## Educational Value

These programs serve as excellent teaching tools for:
- Computer architecture courses
- Performance optimization workshops
- Understanding memory hierarchy effects
- Learning about cache-aware programming
