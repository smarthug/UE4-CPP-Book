# UE4-CPP-Book
이득우의 언리얼 C++ 게임 개발의 정석  4.25.4 버전으로 진행했을때 막히는 부분 정리 

## CHAPTER 6

-  203p ABCharacter.cpp Tick() 

From
```cpp
SpringArm->RelativeRotation = FMath::RInterpTo(SpringArm->GetRelativeRotation(), ArmRotationTo, DeltaTime, ArmRotationSpeed)
```
To
```cpp
SpringArm->SetRelativeRotation(FMath::RInterpTo(SpringArm->GetRelativeRotation(), ArmRotationTo, DeltaTime, ArmRotationSpeed));
```

- 204p ABCharacter.cpp ViewChange() 


From
```cpp
GetController()->SetControlRotation(SpringArm->RelativeRotation);
```
To
```cpp
GetController()->SetControlRotation(SpringArm->GetRelativeRotation());
```


## CHAPTER 8
- 272p 동작하는 4.25.4 버전의 montage UI 
![montage](/img/fixed.png)

- NextAttackCheck 노티파이의 위치가 한 섹션이 끝나는 지점에 가까워질수록 노티파이실행->다음섹션 명령을 내려도 OnMontageEnded 가 실행되서 콤보가 안될 확률이 높다. (출처 - https://blackpinkjisoo.tistory.com/17)


## CHAPTER 11
- 358p ABGameInstance.cpp

FROM
```cpp
  ABCHECK(ABCharacterTAble->RowMap.Num()>0);
```
TO
```cpp
  ABCHECK(ABCharacterTAble->GetRowMap().Num()>0);
```



### Contribution
- https://cafe.naver.com/unrealenginekr/34246?boardType=L