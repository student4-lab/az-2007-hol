# 도서관 앱

## 설명

도서관 앱은 도서관 이용자(회원)와 도서 대출을 관리하는 .NET 9 콘솔 프로그램입니다. 직원은 회원을 검색하고 회원 정보와 대출 내역을 확인할 수 있으며, 회원 갱신, 도서 반납, 대출 기간 연장 작업을 할 수 있습니다. 프로그램은 콘솔 화면, 업무 규칙, 데이터 접근 기능을 각각 나누어 구성하고, JSON 파일을 데이터 저장소로 사용합니다.

## 프로젝트 구조

- `AccelerateDevGHCopilot/` - 도서관 앱 솔루션 폴더입니다.
  - `AccelerateDevGHCopilot.sln` - 여러 프로젝트를 함께 관리하는 솔루션 파일입니다.
  - `src/` - 애플리케이션의 소스 코드가 들어 있습니다.
    - `Library.ApplicationCore/` - 도서관의 핵심 데이터와 업무 규칙을 담당합니다.
      - `Entities/` - 저자, 도서, 도서 사본, 대출, 회원 데이터를 정의합니다.
      - `Enums/` - 대출과 회원 갱신 결과를 나타내는 상태 값을 정의합니다.
      - `Interfaces/` - 데이터 저장소와 업무 서비스가 제공해야 할 기능을 정의합니다.
      - `Services/` - 대출 및 회원 관리 업무 규칙을 처리합니다.
    - `Library.Console/` - 콘솔 화면과 사용자 입력을 담당합니다.
      - `Program.cs` - 의존성을 연결하고 애플리케이션을 시작합니다.
      - `ConsoleApp.cs` - 사용자 입력을 처리하고 화면 상태를 전환합니다.
      - `ConsoleState.cs` - 콘솔 앱의 화면 상태를 정의합니다.
      - `CommonActions.cs` - 사용자가 선택할 수 있는 작업을 정의합니다.
      - `appSettings.json` - JSON 데이터 파일 경로 등의 설정을 저장합니다.
      - `Json/` - 저자, 도서, 도서 사본, 대출, 회원 예제 데이터를 저장합니다.
    - `Library.Infrastructure/` - JSON 파일을 이용한 데이터 접근 기능을 제공합니다.
      - `Data/JsonData.cs` - JSON 데이터를 읽고 저장하며 데이터 간 관계를 구성합니다.
      - `Data/JsonLoanRepository.cs` - 대출 정보를 조회하고 수정합니다.
      - `Data/JsonPatronRepository.cs` - 회원 정보를 검색, 조회, 수정합니다.
  - `tests/` - 애플리케이션의 자동화된 테스트가 들어 있습니다.
    - `UnitTests/` - 업무 서비스의 단위 테스트를 포함합니다.
      - `ApplicationCore/LoanService/` - 대출 반납과 연장 테스트입니다.
      - `ApplicationCore/PatronService/` - 회원 갱신 테스트입니다.
      - `LoanFactory.cs`, `PatronFactory.cs` - 테스트용 데이터를 만듭니다.

## 주요 클래스와 인터페이스

- `ConsoleApp` - 콘솔 사용 흐름과 사용자 작업을 관리합니다.
- `Loan`, `Patron`, `Book`, `BookItem`, `Author` - 도서관의 핵심 데이터를 표현합니다.
- `ILoanService`, `IPatronService` - 대출 및 회원 관리 업무 기능의 계약을 정의합니다.
- `ILoanRepository`, `IPatronRepository` - 대출 및 회원 데이터 접근 기능의 계약을 정의합니다.
- `LoanService` - 대출 반납과 연장에 필요한 업무 규칙을 적용합니다.
- `PatronService` - 회원 갱신에 필요한 업무 규칙을 적용합니다.
- `JsonData` - JSON 파일을 읽고 저장하며 관련 데이터 객체를 구성합니다.
- `JsonLoanRepository`, `JsonPatronRepository` - `JsonData`를 사용해 저장소 기능을 구현합니다.

## 사용 방법

.NET SDK 9.0 이상이 필요합니다.

`LabFiles/02-analyze-document-code` 폴더에서 다음 명령을 실행하면 콘솔 앱을 시작할 수 있습니다.

```bash
dotnet run --project AccelerateDevGHCopilot/src/Library.Console/Library.Console.csproj
```

화면의 안내에 따라 회원을 검색하고 원하는 작업을 선택하세요. 단위 테스트는 다음 명령으로 실행할 수 있습니다.

```bash
dotnet test AccelerateDevGHCopilot/tests/UnitTests/UnitTests.csproj
```

## 라이선스

이 프로젝트는 MIT 라이선스를 따릅니다. 자세한 내용은 저장소의 `LICENSE` 파일을 참고하세요.
