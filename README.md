# Software Engineer

#### Technical Skills: C++, C#, Python, HTML, CSS, Javascript, Flutter/Dart, Unreal Engine, Unity

## Education
- Game Development Bootcamp | Playback Studio (_2023_)								       		
- UE5 C++ Developer course | Udemy/Epic Games (_2022_)	 			        		
- CS50x Computer Science course | Harvard University (_2022_)
- Bachelor of Engineering | University of Portsmouth (_2020_)

## Work Experience
**Gameplay Software Engineer Intern • Nerd Monkeys (_January 2024 - May 2024_)**
- Excellent reasoning and complex problem-solving ability when presented with challenging scripting tasks showing tenacity and taking ownership of my work.
- Showed initiative through debugging and expanding on existing code.
- Tested and improved gameplay features.
- Improved teamwork ability by brainstorming with others how to implement game design ideas into code/gameplay mechanics.

**Founder/Developer/Designer • Bloqi (_February 2023 - March 2024_)**
- Social platform bringing a Twitter-like experience to the TikTok generation in university.
- Managed the product development process from design to beta testing, showcasing strong team spirit and project management skills.
- Designed the UI using Figma. Developed first version of app in Flutter in less than a month.
- Built front-end app infrastructure using GetX state-management, later refactoring to BloC.
- Iterating rapidly on product and associated media enabled progression through multiple stages of King’s College’s Idea Factory Incubator and sustained interest in potential investors and a judge at the finals, achieved through sheer drive and determination.

## Projects

### GPT-2 Clone (124M)

![So Cold Barn](/assets/img/SoColdBarn.png)

Through my own interest and online resources, I recreated OpenAI's GPT-2 on a smaller scale. During this process, I learnt all the accompaning components that make up a neural network and a Large Language Model, such as calculating token weights, logits, loss and gradients during a backwards pass and adjusting the weights to achieve a better loss. I also learnt about different types of optimisation techniques to save on time and space, such as the various weight decay methods as well as forcing calculations on 1 kernel using flash attention. Overall, I believe my practical approach to learning has made me much more confident working with neural networks and understanding how AI works on a deep level.

### 2D Box-Pushing Puzzle Game

![So Cold Barn](/assets/img/SoColdBarn.png)

While working as gameplay programmer at Nerd Monkeys I worked on several projects, one being So Cold Barn. During this time I was introduced to many gameplay programming concepts such as how C# events give more control and allow multiple functions to be called from different scripts. I was also able to improve my teamwork skills and brainstorm with other programmers (some more experienced than me) how we can turn requested features into fruition, mainly via scripting. Along the way, I improved my debugging skills within code and game engine integration. This required a deep understanding of the scripts (including ones I did not work on previously) in order to find the issue and implement a solution. I enjoyed the creativity from working on gameplay features as well finding creative solutions to bugs. Below is a script I made to spawn a number of consumables (pills, in this case) into a level based on the previous level's completion percentage.

    public class FloorPillActivation : MonoBehaviour
    {
        [SerializeField] private GameState _gameState;
        [SerializeField] private GameInfo _gameInfo;
        void Start()
        {
    
            ActivatePillsBasedOnCompletion();
        }

        private void ActivatePillsBasedOnCompletion()
        {
            GameObject [] allPills = GameObject.FindGameObjectsWithTag("Pill");
            Debug.Log("Total pills: " + allPills.Length);
            foreach(GameObject pill in allPills)
            {
                pill.SetActive(false);
            }

            int currentLevelIndex = _gameInfo.CurrentLevel - 1;
            float previousLevelCompletion = _gameState.FloorCompletionPercentages[currentLevelIndex - 1];
        
            float targetPercentage = previousLevelCompletion / 100f;
            Debug.Log("Target percentage: " + targetPercentage);
        

            int numPillsToActivate = Mathf.RoundToInt(targetPercentage * allPills.Length); 

            if (numPillsToActivate > allPills.Length) 
            {
                numPillsToActivate = allPills.Length;
            }

            List activatedPillIndices = new List(); 

            while (activatedPillIndices.Count < numPillsToActivate)
            {
                int randomIndex = Random.Range(0, allPills.Length);
                if (!activatedPillIndices.Contains(randomIndex)) 
                {
                    activatedPillIndices.Add(randomIndex);
                    allPills[randomIndex].SetActive(true);
                    Debug.Log("Selected index: " + randomIndex + ", Activated pills: " + activatedPillIndices.Count);
                }

            }
        }
    }

### 2D Side-Scrolling Platform Game

![Demon Cat](/assets/img/DemonCat.png)

During the Game Development Bootcamp with Playback Studio, we were tasked with making our own complete game. Through trial and error and researching specific features I wanted for my game, I became very comfortable with Unity and C# and I believe this method of learning was much more valuable than doing a course or traditional learning. Such features I explored in this game were: AI enemies, cliff detection, player attack detection, parallax background, particle system, health and damage for characters, player movement, character animations and rigging characters. Below is the C# code for my "damageable" script, which enables my player and enemies to take damage to their health when hit.

    public class Damageable : MonoBehaviour
    {
        public UnityEvent damageableHit;
        public UnityEvent damageableDeath;
        public UnityEvent healthChanged;
        public UIManager gameManager;
        Animator animator;
        [SerializeField]
        private int _maxHealth = 100;
        private bool isDead;
    
        public int MaxHealth
        {
            get
            {
                return _maxHealth;
            }
            set
            {
                _maxHealth = value;
            }
        }
    
        [SerializeField]
        private int _health = 100;
        public int Health
        {
            get
            {
                return _health;
            }
            set
            {
                _health = value;
                healthChanged?.Invoke(_health, MaxHealth);
                if(_health <= 0 && !isDead)
                {
                    isDead = true;
                    IsAlive = false;
                    gameManager.gameOver();
                }
            }
        }
    
        [SerializeField]
        private bool _isAlive = true;
        [SerializeField]
        private bool isInvincible = false;
        private float timeSinceHit = 0;
        public float invincibilityTime = 0.25f;
        public float lockTime = 0.5f;
    
        public bool IsAlive { 
            get
            {
                return _isAlive;
            }
            set
            {
                _isAlive = value;
                animator.SetBool("isAlive", value);
                Debug.Log("IsAlive set " + value);
    
                if(value == false)
                {
                    damageableDeath.Invoke();
                }
            } 
        }
    
        public bool LockVelocity { 
            get 
            {
                return animator.GetBool("lockVelocity");
            }
            set{
                animator.SetBool("lockVelocity", value);
            } 
        }
    
        private void Awake()
        {
            animator = GetComponent();
        }
    
        private void Update()
        {
            if(isInvincible)
            {
                if(timeSinceHit > invincibilityTime)
                {
                    // Remove invincibility
                    isInvincible = false;
                    timeSinceHit = 0;
                }
                timeSinceHit +=Time.deltaTime;
            }
        }
    
        public bool Hit(int damage, Vector2 knockback)
        {
            if(IsAlive && !isInvincible)
            {
                Health -= damage;
                isInvincible = true;
                // Notify other subscribed components that the damageable was hit to handle the knockback
                animator.SetTrigger("hit");
                LockVelocity = true;
                damageableHit?.Invoke(damage, knockback);
                CharacterEvents.characterDamaged.Invoke(gameObject, damage);
    
                return true;
            }
            return false;
        }
        public bool Heal(int healthRestore)
        {
            if(IsAlive && Health < MaxHealth)
            {
                int maxHeal = Mathf.Max(MaxHealth - Health, 0);
                int actualHeal = Mathf.Min(maxHeal, healthRestore);
                Health += actualHeal;
                CharacterEvents.characterHealed(gameObject, actualHeal);
                return true;
            }
            return false;
        }
    }
    

### Bloqi - Text-Based Social Media App

![Bloqi Demo](/assets/img/BloqiDemo40.png)

Figma/Flutter/Dart: UI development of a social platform bringing a Twitter-like experience to the TikTok generation in university. Designed the UI within Figma, to be simple and easy to use. The goal was to be as minimalistic as possible without losing function. I then integrated the UI into a working version of the app using Flutter/Dart with BloC state-management, while stil maintaining the look and feel of the UI/UX and easy navigation with swipe and drag gestures.

### 3D Simple Shooter Game

![Simple Shooter](/assets/img/SimpleShooter.png)

This is a short shooter game where the objective is to kill all the enemies. Developing this game helped me better understand shooting mechanics, AI characters, player and character movement and animation. Syncing animations to character movement and physics in the C++ code proved to be challenging, however after experimentation and research I am much more comfortable with physics and mathematics related functions in C++ as well as the animation tools in Unreal Engine. Below is the C++ "ShooterCharacter" class I used for movement, damage to health and aiming.

    void AShooterCharacter::BeginPlay()
    {
        Super::BeginPlay();
    
        Health = MaxHealth;
    
        Gun = GetWorld()->SpawnActor(GunClass);
        GetMesh()->HideBoneByName(TEXT("weapon_r"), EPhysBodyOp::PBO_None);
        Gun->AttachToComponent(GetMesh(), 
        FAttachmentTransformRules::KeepRelativeTransform, TEXT("WeaponSocket"));
        Gun->SetOwner(this);
    }
    
    bool AShooterCharacter::IsDead() const
    {
        return Health <= 0;
    }
    
    float AShooterCharacter::GetHealthPercent() const
    {
        return Health / MaxHealth;
    }
    
    // Called every frame
    void AShooterCharacter::Tick(float DeltaTime)
    {
        Super::Tick(DeltaTime);
    
    }
    
    // Called to bind functionality to input
    void AShooterCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
    {
        Super::SetupPlayerInputComponent(PlayerInputComponent);
    
        PlayerInputComponent->BindAxis(TEXT("MoveForward"), this, &AShooterCharacter::MoveForward);
        PlayerInputComponent->BindAxis(TEXT("LookUp"), this, &APawn::AddControllerPitchInput);
        PlayerInputComponent->BindAxis(TEXT("LookUpRate"), this, &AShooterCharacter::LookUpRate);
        PlayerInputComponent->BindAxis(TEXT("MoveRight"), this, &AShooterCharacter::MoveRight);
        PlayerInputComponent->BindAxis(TEXT("LookRight"), this, &APawn::AddControllerYawInput);
        PlayerInputComponent->BindAxis(TEXT("LookRightRate"), this, &AShooterCharacter::LookRightRate);
        PlayerInputComponent->BindAction(TEXT("Jump"),EInputEvent::IE_Pressed, this, &ACharacter::Jump);
        PlayerInputComponent->BindAction(TEXT("Shoot"),EInputEvent::IE_Pressed, this, 
        &AShooterCharacter::Shoot);
    }
    
    float AShooterCharacter::TakeDamage(float DamageAmount, struct FDamageEvent const &DamageEvent, 
    class AController *EventInstigator, AActor *DamageCauser)
    {
        float DamageToApply = Super::TakeDamage(DamageAmount, DamageEvent, EventInstigator, 
        DamageCauser);
        DamageToApply = FMath::Min(Health, DamageToApply);
        Health -= DamageToApply;
        UE_LOG(LogTemp, Warning, TEXT("Health left %f"), Health);
        
        if (IsDead())
        {
            ASimpleShooterGameModeBase* GameMode = GetWorld()->GetAuthGameMode();
            if (GameMode != nullptr)
            {
                GameMode->PawnKilled(this);
            }
            DetachFromControllerPendingDestroy();
            GetCapsuleComponent()->SetCollisionEnabled(ECollisionEnabled::NoCollision);
            
            
        }
        return DamageToApply;
    }
    
    void AShooterCharacter::MoveForward(float AxisValue)
    {
        AddMovementInput(GetActorForwardVector() * AxisValue);
    }
    
    void AShooterCharacter::MoveRight(float AxisValue)
    {
        AddMovementInput(GetActorRightVector() * AxisValue);
    }
    
    void AShooterCharacter::LookUpRate(float AxisValue)
    {
        AddControllerPitchInput(AxisValue * RotationRate * GetWorld()->GetDeltaSeconds());
    }
    
    void AShooterCharacter::LookRightRate(float AxisValue)
    {
        AddControllerYawInput(AxisValue * RotationRate * GetWorld()->GetDeltaSeconds());
    }
    
    void AShooterCharacter::Shoot()
    {
        Gun->PullTrigger();
    }

### First Person Puzzle Game

![Crypt Raider](/assets/img/CryptRaider.png)

I created this game to improve my skills using modular level design. Using an asset pack, I designed a dungeon and crypt where the objective of the game is to venture into the dungeon and retrieve a valuable statue. During the process of making this game I became competent in use line traces and collisions as well as debug tools such as a debug sphere. Such tools improved my debugging and problem-solving skills. For example, I came across an issue where my player wound not pick up an item, using common debugging practice as well as engine specific debugging tools I was able to solve this problem by extending the "MaxGrabDistance". I found that even simple issues like this were satisfying to solve and maintained my excitement for programming. Below is the script for the "Grabber" component, where I used tags for when an item is grabbed and debug lines and spheres to see when something is picked up and released and to show the grabbable distance.

    void UGrabber::BeginPlay()
    {
        Super::BeginPlay();
    }
    
    // Called every frame
    void UGrabber::TickComponent(float DeltaTime, ELevelTick TickType, 
    FActorComponentTickFunction* ThisTickFunction)
    {
        Super::TickComponent(DeltaTime, TickType, ThisTickFunction);
    
        UPhysicsHandleComponent* PhysicsHandle = GetPhysicsHandle();
    
        if (PhysicsHandle && PhysicsHandle->GetGrabbedComponent())
        {
            FVector TargetLocation = GetComponentLocation() + GetForwardVector().GetSafeNormal() 
            * HoldDistance;
            PhysicsHandle->SetTargetLocationAndRotation(TargetLocation, GetComponentRotation());
        }
    }
    
    void UGrabber::Grab()
    {
        UPhysicsHandleComponent* PhysicsHandle = GetPhysicsHandle();
        if (PhysicsHandle == nullptr)
        {
            return;
        }
    
        FHitResult HitResult;
        bool HasHit = GetGrabbableInReach(HitResult);
        if (HasHit)
        {
            UPrimitiveComponent* HitComponent = HitResult.GetComponent();
            HitComponent->SetSimulatePhysics(true);
            HitComponent->WakeAllRigidBodies();
            AActor* HitActor = HitResult.GetActor();
            HitActor->Tags.Add("Grabbed");
            HitActor->DetachFromActor(FDetachmentTransformRules::KeepWorldTransform);
            PhysicsHandle->GrabComponentAtLocationWithRotation(
                HitComponent,
                NAME_None,
                HitResult.ImpactPoint,
                GetComponentRotation()
            );
        }
    }
    
    void UGrabber::Release()
    {
        UPhysicsHandleComponent* PhysicsHandle = GetPhysicsHandle();
        
        if (PhysicsHandle && PhysicsHandle->GetGrabbedComponent())
        {
            AActor* GrabbedActor = PhysicsHandle->GetGrabbedComponent()->GetOwner();
            GrabbedActor->Tags.Remove("Grabbed");
            PhysicsHandle->ReleaseComponent();
        }
    }
    
    UPhysicsHandleComponent* UGrabber::GetPhysicsHandle() const
    {
        UPhysicsHandleComponent* Result = GetOwner()->FindComponentByClass();
        if (Result == nullptr)
        {
            UE_LOG(LogTemp, Error, TEXT("Grabber requires a UPhysicsHandleComponent."));
        }
        return Result;
    }
    
    bool UGrabber::GetGrabbableInReach(FHitResult& OutHitResult) const
    {
        FVector Start = GetComponentLocation();
        FVector End = Start + GetForwardVector() * MaxGrabDistance;
        DrawDebugLine(GetWorld(), Start, End, FColor::Red);
        DrawDebugSphere(GetWorld(), End, 10, 10, FColor::Blue, false, 5);
    
        FCollisionShape Sphere = FCollisionShape::MakeSphere(GrabRadius);
        FHitResult HitResult;
        return GetWorld()->SweepSingleByChannel(OutHitResult, Start, End, FQuat::Identity, 
        ECC_GameTraceChannel2, Sphere);  
    }

### 3D Tank Shooter Game

![Toon Tanks](/assets/img/ToonTanks.png)

In this game, you control a small tank and move around to shoot turrets, once all the turrets are destroyed you win the game, however the turrents lock onto you and shoot back when you come within range. While developing this game I learnt how to use a "fire" functionality with projectiles, add special effects like smoke, explosions and SFX and add enemy AI controlled turrets to the game. The projectile class has an "OnHit" function that takes into account the various variables/classes such as: a "HitComp", actor location in space, a vector variable, a damage class and many more to make it work correctly. Taking all these into account made making this feature complicated, but greatly improved my learning by sticking through it and solving issues as they arose. I believe: the more complex, the greater the challenge, the greater the learning potential. This is what makes a better developer. Below is the script for a projectile.

    AProjectile::AProjectile()
    {
        // Set this actor to call Tick() every frame.  You can turn this off to improve performance 
        if you don't need it.
        PrimaryActorTick.bCanEverTick = false;
    
        ProjectileMesh = CreateDefaultSubobject(TEXT("Projectile Mesh"));
        RootComponent = ProjectileMesh;
    
        ProjectileMovementComponent = CreateDefaultSubobject
            (TEXT("Projectile Movement Component"));
        ProjectileMovementComponent->MaxSpeed = 1300.f;
        ProjectileMovementComponent->InitialSpeed = 1300.f;
    
        TrailParticles = CreateDefaultSubobject(TEXT("Smoke Trail"));
        TrailParticles->SetupAttachment(RootComponent);
    }
    
    // Called when the game starts or when spawned
    void AProjectile::BeginPlay()
    {
        Super::BeginPlay();
        
        ProjectileMesh->OnComponentHit.AddDynamic(this, &AProjectile::OnHit);
        if (LaunchSound)
        {
            UGameplayStatics::PlaySoundAtLocation(this, LaunchSound, GetActorLocation());
        }
    }
    
    // Called every frame
    void AProjectile::Tick(float DeltaTime)
    {
        Super::Tick(DeltaTime);
    }
    
    void AProjectile::OnHit(UPrimitiveComponent* HitComp, AActor* OtherActor, UPrimitiveComponent* 
    OtherComp, FVector NormalImpulse, const FHitResult& Hit)
    {
        AActor* MyOwner = GetOwner();
        if (MyOwner == nullptr) 
        {
            Destroy();
            return;
        }
    
        AController* MyOwnerInstigator = MyOwner->GetInstigatorController();
        UClass* DamageTypeClass = UDamageType::StaticClass();
    
        if (OtherActor && OtherActor != this && OtherActor != MyOwner)
        {
            UGameplayStatics::ApplyDamage(OtherActor, Damage, MyOwnerInstigator, this, 
            DamageTypeClass);
            if (HitParticles)
            {
                UGameplayStatics::SpawnEmitterAtLocation(this, HitParticles, GetActorLocation(), 
                GetActorRotation());
            }
            if(HitSound)
            {
                UGameplayStatics::PlaySoundAtLocation(this, HitSound, GetActorLocation());
            }
            if (HitCameraShakeClass)
            {
                GetWorld()->GetFirstPlayerController()->ClientStartCameraShake(HitCameraShakeClass);
            }
        }
        Destroy();
    }
