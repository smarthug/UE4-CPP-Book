## Chap12

- 432p - 오류가 아닌 팁 [#3](https://github.com/smarthug/UE4-CPP-Book/issues/3) 참고
- possessedBy 를 override 하면은 원래의 possessedBy 에서 자동으로 처리해주던 부분을 수동으로 해야합니다. 
ABCharacter 생성자 -> AI Controller 빙의 -> PossessedBy 순서로 진행되는데 
AI 컨트롤러가 빙의되면서 컨트롤 설정이 바뀌고 바뀐 설정을 재설정 해야합니다.
그래서 생성자에서 이미 호출한 SetControlMode(EControlMode::Diablo) 를 PossessedBy 에서 또 호출할 필요가 있는것입니다.
```cpp
void AABCharacter::PossessedBy(AController* NewController)
{
	Super::PossessedBy(NewController);

	if (IsPlayerControlled())
	{

		SetControlMode(EControlMode::DIABLO);
		GetCharacterMovement()->MaxWalkSpeed = 600.0f;
	}
	else
	{
		SetControlMode(EControlMode::NPC);
		GetCharacterMovement()->MaxWalkSpeed = 300.0f;
	}
}
```