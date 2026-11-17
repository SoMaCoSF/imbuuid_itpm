<!-- SOM-DOC-10846-v1.0.0 · Ghost Catalog · SoMaCoSF -->
# STATE — Spoken ITPM (SOM-DOC-10845), graded snapshot 2026-11-17

Cold-landing state for any agent joining this build. Grades: VM-PROVEN = exercised on the build VM; UNVERIFIED = not yet exercised.

- T1 INGEST — COMPLETE (VM-PROVEN). DXF (ezdxf) + PDF (PyMuPDF) → addressed records under the record contract; 23 records on the sample building (DXF 11, PDF 12), provenance 100%, tests 7/7. DWG + IFC inputs refused at this tier (exit 3) — see the native tier.
- T2 BIM/BOM + COMMISSIONING — COMPLETE (VM-PROVEN). BOM rollup (system → type → tag), commissioning instances, trade chain GC→STRUCT→MEP→LV→IT proven, tests 8/8. Ran on fixtures; run against T1's real records is T5's job.
- T3 SPOKEN ENGINE — COMPLETE (VM-PROVEN). Deterministic grammar → typed actions (SHOW/HIDE/FIND/LIST_BOM/PUNCHLIST/COMMISSION/MEASURE/STATUS), zero LLM calls, tests 18/18. Consumes transcript text; the surface does speech-to-text.
- T4 PLAN SURFACE — COMPLETE, NOT DEPLOYED (founder tap). `/plans` in the ITPM app: SVG plan canvas from records, gloss-first element cards, command bar, site-video slot, GIS strip. Fixture records; JSONL→JSON adapter for T1 records still owed.
- T1b NATIVE TIER — IN FLIGHT. DWG route PROVEN: ODA File Converter round-trip DXF→DWG→DXF preserved layers 8/8, entities 18/18, all tags; records stamped route:oda-file-converter. Caveat: ODA's published terms restrict non-member use to non-commercial — founder/legal read owed before commercial reliance. IFC UNBLOCKED: FreeCAD 1.1.4 AppImage bundles IfcOpenShell 0.8.4, exercised standalone (VM-PROVEN). FreeCAD/LibreCAD/Blender downloaded, sha256-verified, exercised headless. Revit viewer-mode IFC export + eDrawings COM route: UNVERIFIED (need a Windows node).
- ARCHITECTURE — RULED: Route C HYBRID. Native Rust GIS (`rustgis-itpm`) owns truth, IMBUUID addressing, spatial indexing, interpretation; Blender is a swappable headless render backend, never source of truth. Python prototype of the index: tests 19/19 on real records. Rust port is build-order step 1.
- REA PATTERN (from SoMaCoSF/rea re-eval) — native readers only for openly specified formats (DXF/PDF/IFC); harness vendor engines for proprietary ones (DWG/RVT/SLDPRT). rea itself has zero CAD/BIM/GIS capability; the pattern transfers, not the code.
- T5 INTEGRATION — PENDING. T2 + T3 against T1's real records, end-to-end: ingest → "commission AHU-1" → instance minted → "punchlist the west door" → record.
- INFRA NOTE — the build VM's home disk is under a hard per-user quota failure (writes fail, filesystem not full). This coord tree was therefore written directly to GitHub via the API. Local landing follows when quota clears.
- OPEN FOUNDER DECISIONS — APS (Autodesk) narrowed to fallback-only (needed only if both the Windows-node Revit-viewer IFC route and the FreeCAD/IfcOpenShell route fail); ODA license read; Windows node session; /plans deploy.
