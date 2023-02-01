# Hypno.exe Technical Documentation

## Overview

## Class Diagrams

### Program Classes
```mermaid
classDiagram
direction LR

class FHCBaseInfo~struct~{
    +FText Name
    +FText Description
    +FGameplayTagContainer Platforms
    +FHCTagContainer Tags
    +TSoftObjectPtr<UTexture2D> Image
    +UTexture2D* GetImage()
    +void SetImage(UTexture2D* InImage)
}

class EHCElementState~enum : uint8~{
    0x00 : NotRunning
	0x01 : Running
	0x02 : MAX
}

class AHCElementBase{
    -EHCElementState State
    -bool bDoesTick
    +FHCBaseInfo Info
    +EHCElementState GetElementState()
    +void TickElement(float DeltaTime)
    +void StartElement()
    +void PauseElement()
    +void StopElement()
    +void DestroyElement(EHCDestroyReason Reason)
}

class UHCElementEditorWidget{
    +StartElement() void
}

class UHCElementDataBase{
    +TSubclassOf<AHCElementBase> ElementClass
    +TSubclassOf<UHCElementEditorWidget> EditorWidget
    -AHCElementBase* ElementActor
    ~UHCElementDataBase* CreateElementData(UObject* Outer)
    ~void SetElementData(UHCElementDataBase* Target, UStruct* ElementData)
    +void ProcessElementData(UHCElementDataBase* Target, FProperty* Property, void* StructPtr)
    +void OnNewElementData(FHCElementSettingsBase NewData)
}

class AHCGameModeBase{
    -FRCProgramData CurrentProgram
    +void SetCurrentProgram(FHCProgramData InProgram)
    +FHCProgramData GetCurrentProgram()
    +bool StartProgram()
    +bool PauseProgram()
    +bool PlayProgram()
    +bool StopProgram()
    +bool GoToProgramStart()
    +bool GoToProgramEnd()
    +bool GoForwardOneStage()
    +bool GoBackOneStage()
}

class AHCGameStateBase{
    -TArray<AHCElementBase*> Elements
    +FGuid CreateElement(FHCElementData Element) Replicated
    +bool DestroyElement(FGuid ElementId) Replicated
    +void DestroyAllElements() Replicated
}
```

## Primary Processes

### Program Playback

```mermaid
sequenceDiagram

participant GameMode
participant GameState
participant ElementData
participant ElementActor

GameMode ->> GameMode : ProgramData Set

loop Per-Stage
    loop Per-Element
        GameMode ->> GameState : Trigger Spawn Data
        GameState ->> ElementData : Spawn
        ElementData ->> ElementData : Load Content
        ElementData ->> GameState : Report Loaded
        GameState ->> GameMode : Report Loaded
    end
end

GameMode ->> GameMode : Play Program

loop Per-Stage

    GameMode ->> GameMode : Start Stage

    loop Per-Element
        GameMode ->> GameState : Request Spawn
        GameState ->> ElementData : Request Spawn
        ElementData ->> ElementActor : Spawn with Data
        ElementActor ->> ElementActor : Initialize Visuals
    end

    GameMode ->> GameMode : Stage End

    loop Per-Element
        GameMode ->> GameState : Destroy Element
        GameState ->> ElementData : Request Destroy
        ElementData ->> ElementActor : Destroy
    end
end

GameMode ->> GameMode : End Program

```

### Program Library

### Program Editing

#### Add Stage

#### Remove Stage

#### Add Element

#### Edit Element

#### Remove Element

### Program Exporting

### Program Importing
