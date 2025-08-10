Wotlk-Server (AzerothCore Fork) – Module-first
Personal fork of AzerothCore focused on creating custom modules (Raids, Instances, RP features).
This fork is for educational and training purposes during my apprenticeship as an IT Specialist for System Integration.

Goals of this Fork

Module-first: New content (NPCs, Items, Quests, Events, Raids/Instances, RP systems) will not be merged directly into the core but developed as standalone modules.

Clean Core: Keep the core as close to upstream AzerothCore as possible to make merging updates easy.

Learning Project: Building, maintaining, and extending a WoW 3.3.5a server as part of my apprenticeship (starting 08/2025). Focus: Build/CI, C++ scripting, SQL, structure & server operation.

Repository Overview
Wotlk-Server/
├─ modules/ # all active modules (submodules or direct code)
│ ├─ mod-individual-progression/
│ ├─ mod-autobalance/
│ ├─ mod-transmog/
│ ├─ mod-account-achievements/
│ ├─ mod-npc-enchanter/ # example
│ └─ mod-... # own content (Raids/Instances/RP)
├─ src/server/scripts/ # Core scripts (keep unchanged if possible)
├─ data/sql/custom/ # only minor SQL adjustments; main content in modules
├─ conf/dist/ # sample configs (no passwords)
└─ README.md

Note: Build artifacts, real passwords, and private data are excluded via .gitignore.

Roadmap (Excerpt)
Raids / Instances as Modules

Halion clone & CoA portals as standalone module

Phase / progression control per instance

RP Modules

Portal & travel systems, social features, guild QoL

Global Server Progression

WotLK Phases P1 → P4 switchable via SQL/config

Tools & Quality

Consistent module structure, clear SQL migration paths

(Optional) simple CI for module builds

Creating Modules (Guidelines)
Name scheme: modules/mod-<short-purpose>/

Minimal structure:
modules/mod-example/
├─ CMakeLists.txt
├─ README.md
├─ conf/mod-example.conf.dist
├─ sql/
│ ├─ world/ # world changes
│ ├─ auth/ # auth changes (rare)
│ └─ characters/
└─ src/
└─ ModExample.cpp # RegisterModule(), hooks, scripts

C++ skeleton example:
#include "ScriptMgr.h"
#include "Chat.h"

class ModExample : public ModuleScript
{
public:
ModExample() : ModuleScript("mod-example") {}

cpp
Kopieren
Bearbeiten
void OnAfterConfigLoad(bool /*reload*/) override  
{  
    // Load/check config  
}  
};

void Addmod_exampleScripts()
{
new ModExample();
}

CMake (inside module):
ac_add_module(mod-example
SOURCES
src/ModExample.cpp
)

SQL migrations:

Each change as a separate file with date prefix (e.g. 2025_08_01_00_world_init.sql)

Only create/alter module-specific tables/entries

Quick Start (Windows)

Requirements: Visual Studio, Git, CMake, MySQL, OpenSSL, Boost

Clone repository:
git clone https://github.com/bloody2927/Wotlk-Server.git

Place/activate modules in modules/

Create build folder & configure CMake:
mkdir build && cd build
cmake .. -A x64 -DCMAKE_BUILD_TYPE=RelWithDebInfo
cmake --build . --config RelWithDebInfo -j

Import DB (AzerothCore standard) + apply module SQLs

Copy and adjust worldserver.conf/authserver.conf from conf/dist

Note: .gitignore hides real *.conf with passwords

Keeping Upstream Updated
git remote add upstream https://github.com/azerothcore/azerothcore-wotlk.git
git fetch upstream
git checkout main
git merge upstream/master # or rebase if preferred
git push

Develop your own changes preferably in feature branches and merge them via PR into your fork.

Contributions / Issues
This repo is primarily for my learning/training project.
Feedback and suggestions are welcome (via Issue), PRs after discussion.
For contributing to the main project, please follow AzerothCore Contributing Guides.

License & Credits

Core is licensed under GNU AGPL v3

Parts based on MaNGOS/Trinity/Sunwell are under GNU GPL v2

See LICENSE and the original repo for full details
Credits: All recognition to the AzerothCore team and community
This fork is not supported by Blizzard. Use at your own risk.

Contact

Discord (AzerothCore Community): https://discord.gg/gkt4y2x

Fork owner: bloody2927 – usage for educational/training purposes (IT Specialist System Integration)
