# UE4-CPP-Book
이득우의 언리얼 C++ 게임 개발의 정석  4.25.4 버전으로 진행했을때 막히는 부분 정리.  [정오표](http://www.acornpub.co.kr/book/unreal-c#errata)에 없는 부분만 작성하였습니다.  

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

## CHAPTER 12
- 399p ABAIController.h

FROM
```cpp
  virtual void Possess(APawn* InPawn) override;
  virtual void UnPossess() override;
```
TO
```cpp
  virtual void OnPossess(APawn* InPawn) override;
  virtual void OnUnPossess() override;
```

- 400p ABAIController.cpp

FROM
```cpp
void AABAIController::Possess(APawn* InPawn)
{
	Super::Possess(InPawn);
	...
}

void AABAIController::UnPossess()
{
	Super::UnPossess();
	...
}
```
TO
```cpp
void AABAIController::OnPossess(APawn* InPawn)
{
	Super::OnPossess(InPawn);
	...
}

void AABAIController::OnUnPossess()
{
	Super::OnUnPossess();
	...
}
```



- 444p
```cpp
public:
	...
	void Attack();
	FOnAttackEndDelegate OnAttackEnd;

private:
	...
	// 원래 선언되어있던 Attack 함수 주석 처리하거나 없애기
	/*void Attack();*/ 
```

## Chapter 13
- 470p 
- ... 생략됨 , 기존에 있던거 지우지말기
```cpp
void AABCharacter::BeginPlay()
{
	Super::BeginPlay();

	...
}
```

## Chapter 14

- 505,6,7p


FROM
```cpp
bCanBeDamaged = false;
bCanBeDamaged = true;
```
TO
```cpp
SetCanBeDamaged(true);
SetCanBeDamaged(false);

```


- 510p


FROM
```cpp
void AABAIController::Possess(APawn* InPawn)
{
	Super::Possess(InPawn);
}
```
TO
```cpp
void AABAIController::OnPossess(APawn* InPawn)
{
	Super::OnPossess(InPawn);
}

```


- 538p

FROM
```cpp
float AABCharacter::TakeDamage(float DamageAmount, FDamageEvent const& DamageEvent, AController* EventInstigator, AActor* DamageCauser)
{
	...
	auto ABPlayerController = Cast<AABPlayerController>(EventInstigator);
	ABCHECK(nullptr != ABPlayerController, 0.0f);
	ABPlayerController->NPCKill(this);
}
```
TO
```cpp
float AABCharacter::TakeDamage(float DamageAmount, FDamageEvent const& DamageEvent, AController* EventInstigator, AActor* DamageCauser)
{
	...
	auto instigator = Cast<AABPlayerController>(EventInstigator);
	ABCHECK(nullptr != instigator, 0.0f);
	instigator->NPCKill(this);
}

```

## Chapter 15

- 597p

FROM
```cpp
if (bIsPlayer)
	{
		auto ABPlayerState = Cast<AABPlayerState>(PlayerState);
		
	}
```
TO
```cpp
if (bIsPlayer)
	{
		auto ABPlayerState = Cast<AABPlayerState>(GetPlayerState());
		
	}
```

### Contribution
- 정오표 http://www.acornpub.co.kr/book/unreal-c#errata
