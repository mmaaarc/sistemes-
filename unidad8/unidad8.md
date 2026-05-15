# Introducció a RAID en entorns Windows

Els RAID (Redundant Array of Independent Disks) són tècniques per combinar diversos discs físics en una unitat lògica amb l'objectiu de millorar el rendiment, la capacitat o la tolerància a fallades.

A Windows i Windows Server, el RAID es pot implementar de dues maneres principals:

- **RAID per programari**: a través del Gestor de discs (Disk Management) o Storage Spaces.
- **RAID per maquinari**: mitjançant una controladora RAID configurada des del BIOS/UEFI o eines del fabricant.

## Tipus de RAID habituals a Windows

> ⚠️ **Nota:** Windows no suporta RAID 6 per programari. Aquest nivell només està disponible mitjançant controladores RAID avançades.

## Storage Spaces (Windows 10/11 i Server)

Storage Spaces és la solució moderna de RAID per programari integrada a Windows i Windows Server.

### Tipus de configuració disponibles:

- **Simple (RAID 0)**: Només distribueix dades. No tolera fallades.
- **Mirall doble o triple (RAID 1/1+)**: Redundància a 2 o 3 còpies.
- **Paritat**: Similar al RAID 5. Protegeix contra fallada d'1 disc (o 2 amb doble paritat en Windows Server).

### Avantatges de Storage Spaces:

- Reconfiguració en calent (hot swap).
- Alertes i supervisió des del tauler de control.
- Integració amb ReFS (Resilient File System) per a entorns crítics.

## Consideracions a l'hora de configurar RAID a Windows

- 🔧 **Uniformitat de discs**: És recomanable utilitzar discos de la mateixa mida, velocitat i tipus.
- 🧱 **Planificació prèvia**: El tipus de RAID escollit determinarà la redundància, rendiment i capacitat útil.
- 🔁 **Còpies de seguretat**: RAID no substitueix una política de còpies de seguretat. Cal tenir backups externs.

## Comparativa: RAID per maquinari vs RAID per programari (Windows)

| Característica | RAID per maquinari | RAID per programari (Storage Spaces) |
|---|---|---|
| Cost | Alt (requereix controladora) | Baix (inclòs al SO) |
| Rendiment | Superior | Acceptable per a la majoria de casos |
| Independència del SO | Sí | No |
| Facilitat de gestió | Depèn del fabricant | Senzilla (Tauler de control) |
| Compatibilitat | Alta | Limitada a Windows |

## Recursos útils

- [Configuració de Storage Spaces a Windows (Microsoft Docs)](https://learn.microsoft.com/windows-server/storage/storage-spaces/)
- [RAID vs Storage Spaces – Comparativa tècnica (TechNet)](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn387076(v=ws.11))
- [ZFS a Windows (projectes alternatius)](https://openzfs.org)
