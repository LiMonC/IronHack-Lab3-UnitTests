# IronHack-Lab3-UnitTests
Repositorio de Laboratorio 3 de IronHack: Unit Test

# Lab: Effective Test Writing Techniques

## Lab Overview and Setup:

This lab aims to sharpen your abilities in applying effective test writing techniques. You’ll focus on enhancing clarity, simplicity, and robustness in test cases. By evaluating and refining provided test scenarios, you’ll practice optimizing test effectiveness using principles from your previous training.

- Introduction to the lab’s objectives and setup in a simulated testing environment where pseudocode or Java can be utilized.
- Access to reference materials and tools that support the test scenarios will be provided.

### Test Case Analysis and Refinement

**Tasks:**
1. **Analysis:** Review the provided test cases that simulate common functionalities but contain deliberate flaws or inefficiencies.
2. **Refinement:** Improve these test cases using both theoretical insights and practical applications from previous lessons.

## Scenarios for Test Case Analysis

### Scenario 1: User Authentication Tests

**Original Test Case (Pseudocode):**
```pseudocode
TEST UserAuthentication
  ASSERT_TRUE(authenticate("validUser", "validPass"), "Should succeed with correct credentials")
  ASSERT_FALSE(authenticate("validUser", "wrongPass"), "Should fail with wrong credentials")
END TEST
```

#### Analysis Report
- **Nombres poco descriptivos:** El nombre  "UserAuthentication" es demasiado genérico.
- **Multiples afirmaciones en una sola prueba:** El test verifica un valid pass y un wrong pass en una sola prueba.
- **Faltan pruebas unitarias:** Faltan validar mas test unitarios. 

#### Improved Test Case
```pseudocode
TEST TestUserAuthentication_ShouldReturnTrueWithValidCredentials
   ASSERT_TRUE(authenticate("validUser", "validPass"), "Should succeed with correct credentials")
END TEST

TEST TestUserAuthentication_ShouldReturnFalseWithInvalidPass
   ASSERT_FALSE(authenticate("validUser", "wrongPass"), "Should fail with wrong credentials")
END TEST

TEST TestUserAuthentication_ShouldReturnFalseWithInvalidUser
  ASSERT_FALSE(authenticate("wrongUser", "validPass"), "Should fail with wrong user")
END TEST

TEST TestUserAuthentication_ShouldReturnFalseWithInvalidCredentials
  ASSERT_FALSE(authenticate("wrongUser", "wrongPass"), "Should fail with wrong user and password")
END TEST

TEST TestUserAuthentication_ShouldReturnFalseWithEmptyCredentials
  ASSERT_FALSE(authenticate("", ""), "Should fail with empty credentials")
END TEST
```

**Rationale:**
- Claridad de nombres mejorada, cada test prueba una sola funcionalidad y se prueban mas casos. 

### Scenario 2: Data Processing Functions

**Original Test Case (Pseudocode):**
```pseudocode
TEST DataProcessing
  DATA data = fetchData()
  TRY
    processData(data)
    ASSERT_TRUE(data.processedSuccessfully, "Data should be processed successfully")
  CATCH error
    ASSERT_EQUALS("Data processing error", error.message, "Should handle processing errors")
  END TRY
END TEST
```

#### Issues in the Original Test Case
- **Nombres poco descriptivos:** El nombre  "DataProcessing" es demasiado genérico.
- **Multiples afirmaciones en una sola prueba:**  El test está tratando de probar 2 casos diferentes y al mismo tiempo un exception handling.

#### Improved Test Case
```pseudocode
TEST TestDataProcessing_ShouldReturnSuccess
  DATA data = fetchData()
  processData(data)
  ASSERT_TRUE(data.processedSuccessfully, "Data should be processed successfully")
END TEST

TEST TestDataProcessing_ErrorHandling
  DATA data = fetchErrorData()
  TRY
    processData(data)
  CATCH error
    ASSERT_EQUALS("Data processing error", error.message, "Should handle processing errors")
  END TRY
END TEST
```

**Rationale:**
- Claridad de nombres mejorada, cada test prueba una sola funcionalidad y se prueban mas casos. 

### Scenario 3: UI Responsiveness

**Original Test Case (Pseudocode):**
```pseudocode
TEST UIResponsiveness
  UI_COMPONENT uiComponent = setupUIComponent(1024)
  ASSERT_TRUE(uiComponent.adjustsToScreenSize(1024), "UI should adjust to width of 1024 pixels")
END TEST
```

#### Issues in the Original Test Case
- **Nombres poco descriptivos:** El nombre  "UIResponsiveness" es demasiado genérico.
- **Multiples afirmaciones en una sola prueba:**  El test está tratando de probar 1 casos diferentes de tamaño de pantalla, limitando las pruebas en diferentes escenarios.


#### Improved Test Case
```pseudocode
TEST  UIResponsiveness_ShouldReturnTrueAtDifferentScreenSizes(numPixels)
  UI_COMPONENT uiComponent = setupUIComponent(numPixels)
  ASSERT_TRUE(uiComponent.adjustsToScreenSize(numPixels), "UI should adjust to width of 1024 pixels")
END TEST
```

**Rationale:**
Se pueden correr los tests a diferentes tamaños de pantalla para probar con diferentes pixeles, asegurandonos de verficiar el comportamiento de cada caso especifico.
