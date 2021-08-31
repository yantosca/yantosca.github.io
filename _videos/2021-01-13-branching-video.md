---
title: "GEOS-Chem 13.0.0: Managing Branches beteween Superproject and Submodules"
collection: videos
type: "Youtube Video tutorial"
permalink: /videos/2021-01-13-branching-video
date: 2021-01-13
---

<iframe width="745" height="418" src="https://www.youtube.com/embed/1fhI-HObyV4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

GEOS-Chem 13.0.0 now uses lightweight wrappers (GCClassic, GCHP) to envelop the GEOS-Chem and HEMCO code as submodules.  Using GCClassic as an example, this video (presented by GEOS-Chem Support Team member Bob Yantosca) will walk you through the process of 

  1. Creating Unix aliases for Git commands; 
  2. Creating a branch in the GEOS-Chem "science codebase" submodule in which you can place your own source code modifications; 
  3. Creating a corresponding branch in the GCClassic superproject that will point to the branch you created in the GEOS-Chem submodule; 
  4. Switching between branches in the GCClassic superproject folder; and 
  5. Using the git submodule update command to fetch commits from the submodules.We demonstrate how to download the GEOS-Chem "Classic" source code and how to use a "dry-run" to download the required input files (e.g. met fields, emissions) to your computer system.  This video applies to GEOS-Chem 13.2.1 and later versions.
