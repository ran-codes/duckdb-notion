# Build Instructions for DuckDB Notion Extension

## ✅ Migration Complete!

All your work has been successfully migrated to the official DuckDB extension template structure.

## 📍 New Project Location

```
D:\GitHub\duckdb-notion
```

## 🔨 Building the Extension

### Prerequisites Check

You need these installed:
- ✅ Git (you have this)
- ✅ Python 3 (you have this)
- ❌ CMake (need to install)
- ❌ Make or Ninja (need to install)
- ❌ C++ Compiler (need to install)

### Install Build Tools (Windows)

**Option 1: Using Chocolatey**
```powershell
# Run in PowerShell as Administrator
choco install cmake ninja
```

**Option 2: Using MSYS2 (Recommended)**
```bash
# In MSYS2 MINGW64 terminal
pacman -S mingw-w64-x86_64-cmake mingw-w64-x86_64-ninja mingw-w64-x86_64-gcc
```

**Option 3: Manual Download**
- CMake: https://cmake.org/download/
- Build Tools: https://visualstudio.microsoft.com/downloads/ (Build Tools for Visual Studio)

### Build Commands

Once you have CMake installed:

**Standard Build:**
```bash
cd /d/GitHub/duckdb-notion
make
```

**Fast Build (with Ninja):**
```bash
cd /d/GitHub/duckdb-notion
GEN=ninja make
```

**Manual CMake Build:**
```bash
cd /d/GitHub/duckdb-notion
mkdir -p build/release
cd build/release
cmake -DCMAKE_BUILD_TYPE=Release ../..
cmake --build . --config Release
```

### Expected Output

After successful build:
```
build/release/extension/notion/notion.duckdb_extension
```

## 🧪 Testing the Extension

### Option 1: R (Quarto Notebook)

1. Open RStudio or R
2. Navigate to the project
3. Open: `_notebooks/donuts-test-traditional.qmd`
4. Make sure `.env` has your Notion token
5. Render the notebook

The notebook will:
- Load the extension from `build/release/extension/notion/notion.duckdb_extension`
- Connect to your Notion test databases
- Query the Products database
- Display results

### Option 2: Command Line

```bash
# Start DuckDB
./build/release/duckdb

# In DuckDB shell
LOAD 'build/release/extension/notion/notion.duckdb_extension';
SELECT * FROM read_notion('487eff84a3444c999f9ca9b7a0b8a80c');
```

### Option 3: Python

```python
import duckdb

con = duckdb.connect()
con.execute("LOAD 'build/release/extension/notion/notion.duckdb_extension'")

# Query your Notion Products database
products = con.execute("""
    SELECT * FROM read_notion('487eff84a3444c999f9ca9b7a0b8a80c')
""").df()

print(products)
```

## 📁 What's in the New Location

```
duckdb-notion/
├── CMakeLists.txt              ✅ Updated with all sources
├── Makefile                    ✅ Official template build system
├── src/
│   ├── notion_extension.cpp    ✅ Main entry point
│   ├── notion_auth.cpp         ✅ Authentication
│   ├── notion_requests.cpp     ✅ API communication
│   ├── notion_read.cpp         ✅ Read function
│   ├── notion_write.cpp        ✅ Write function
│   ├── notion_utils.cpp        ✅ Utilities
│   └── include/*.hpp           ✅ All headers
├── _notebooks/                 ✅ Quarto test notebooks
│   └── donuts-test-traditional.qmd  ← START HERE
├── docs/                       ✅ Documentation website
├── README.md                   ✅ Main docs
├── TESTING_GUIDE.md            ✅ Donut shop test guide
├── .env                        ✅ Your secrets (with DB IDs)
└── duckdb/                     ✅ DuckDB submodule
```

## 🎯 Quick Start Guide

1. **Install build tools** (see above)

2. **Build the extension:**
   ```bash
   cd D:\GitHub\duckdb-notion
   make
   ```

3. **Add your Notion token to `.env`:**
   ```bash
   NOTION_TOKEN=secret_your_actual_token_here
   ```

4. **Test with R/Quarto:**
   ```bash
   cd _notebooks
   quarto render donuts-test-traditional.qmd
   ```

5. **Open the rendered HTML** to see results!

## 🔧 Troubleshooting

### Build Fails

**"cmake: command not found"**
- Install CMake (see Prerequisites above)

**"make: command not found"**
- Use manual cmake build (see Build Commands)
- Or install make/ninja

**"OpenSSL not found"**
- Already configured in `vcpkg.json`
- Will be auto-installed if you have vcpkg

### Extension Won't Load

**Check the path:**
```bash
ls build/release/extension/notion/notion.duckdb_extension
```

**Use absolute path in R:**
```r
ext_path <- normalizePath("build/release/extension/notion/notion.duckdb_extension")
dbExecute(con, sprintf("LOAD '%s'", ext_path))
```

## 📊 Your Test Databases (Already Configured)

In `.env`:
```
NOTION_PRODUCTS_DB=487eff84a3444c999f9ca9b7a0b8a80c
NOTION_ORDERS_DB=221817babd8f4718b885e69ff7007282
NOTION_ORDER_ITEMS_DB=d7dcf04d1f0e45c3b948abd3cc78ebe6
NOTION_SUPPLIERS_DB=810cb65cba0045a38abd5eddfd31d010
```

These are your donut shop test databases in Notion!

## 🚀 Next Steps

1. ✅ Migration complete
2. ⏳ Install build tools (CMake, Make/Ninja)
3. ⏳ Run `make` to build
4. ⏳ Test with Quarto notebook
5. ⏳ Query your Notion databases!

---

**Everything is ready - you just need to build it!** 🎉
