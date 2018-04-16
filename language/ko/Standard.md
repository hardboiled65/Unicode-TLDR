유니코드 3줄 요약<!--- Unicode TL;DR -->
=============
유니코드 표준 문서는 너무 깁니다. 그래서 아마 여러분은 읽지 않으셨겠지요.
그런 여러분(물론 저 또한)을 위해 제가 간단하게 요약했습니다!

_3줄 요약은 TL;DR(Too long; didn't read)의 의역입니다. 실제 3줄 보다 짧거나
길 수도 있어요.^^_<!--- Only for ko -->

목차<!--- Index -->
-----

1. [Introduction](#1-introduction)
    * 1.1  [Coverage](#11-coverage)
        - [Standards Coverage](#standards-coverage)
        - [New Characters](#new-characters)
    * 1.2  [Design Goals](#12-design-goals)
    * 1.3  [Text Handling](#13-text-handling)
        - [Characters and Glyphs](#characters-and-glyphs)
        - [Text Elements](#text-elements)
2. [General Structure](#2-general-structure)
    * 2.1  [Architectural Context](#21-architectural-context)
        - [Basic Text Processes](#basic-text-processes)
        - [Text Elements, Characters, and Text Processes](#text-elements-characters-and-text-processes)
        - [Text Processes and Encoding](#text-processes-and-encoding)
    * 2.2  [Unicode Design Principles]
        - Universality
        - Efficiency
        - Characters, Not Glyphs
        - Semantics
        - Plain Text
        - Logical Order
        - Unification
        - Dynamic Composition
        - Stability
        - Convertibility
    * 2.3  [Compatibility Characters]
        - Compatibility Variants
        - Compatibility Decomposable Characters
    * 2.4  [Code Points and Characters]
        - Types of Code Points
    * 2.5  [Encoding Forms]
        - UTF-32
        - UTF-16
        - UTF-8
        - Comparison of the Advantages of UTF-32, UTF-16, and UTF-8
    * 2.6  [Encoding Schemes]
    * 2.7  [Unicode Strings]
    * 2.8  [Unicode Allocation]
        - Planes
        - Allocation Areas and Blocks
        - Assignment of Code Points
    * 2.9  [Details of Allocation]
        - Plane 0 (BMP)
        - Plane 1 (SMP)
        - Plane 2 (SIP)
        - Other Planes
    * 2.10  [Writing Direction]
    * 2.11  [Combining Characters]
        - Sequence of Base Characters and Diacritics
        - Multiple Combining Characters
        - Ligated Multiple Base Characters
        - Exhibiting Nonspacing Marks in Isolation
        - “Characters” and Grapheme Clusters
    * 2.12  [Equivalent Sequences]
        - Normalization
        - Decompositions
        - Non-decomposition of Certain Diacritics
    * 2.13  [Special Characters]
        - Special Noncharacter Code Points
        - Byte Order Mark (BOM)
        - Layout and Format Control Characters
        - The Replacement Character
        - Control Codes
    * 2.14  [Conforming to the Unicode Standard]
        - Characteristics of Conformant Implementations
        - Unacceptable Behavior
        - Acceptable Behavior
        - Supported Subsets


1\. Introduction
-----------------
**소개**

유니코드는 글 작성을 위한 전세계 공통의 문자 인코딩 표준입니다.
어떤 언어의 어느 문자를 쓰더라도 별도의 이스케이프 문자를 필요로 하지 않습니다.

### 1.1 Coverage
**적용 범위**

유니코드 10.0 버전에서는 전세계 문자들의 136,690개를 포함합니다.
문자로 볼 수 잆는 것들은 포함하지 않습니다.

#### Standards Coverage
**표준 적용 범위**

추가할것

#### New Characters
**새로운 문자들**

유니코드는 각 문화들의 문자의 발견과 연구에 따라 계속해서 새로운 문자들을 추가해
나갑니다.

### 1.2 Design Goals
**설계 목표**

- 범용성: 모든 주요 국제 표준들을 포괄할 수 있을 만큼 커야 합니다.
- 효율성: 고정된 문자 코드는 효율적인 정렬, 검색, 표시 그리고 편집을 가능케 합니다.
- 명확성: 어떤 유니코드 문자 코드도 모호함 없이 같은 문자를 가리켜야 합니다.

### 1.3 Text Handling
**글 다루기**

유니코드의 명세는 다음을 위한 표준 방법을 포함합니다.
- 단어/행을 구분해 냅니다.
- 다른 언어들 사이에 정렬을 합니다.
- 숫자, 날짜, 시간 및 여러 로케일 간의 요소들을 포맷합니다.
- 아랍 문자, 히브리 문자와 같은 우측부터 쓰는 언어의 글을 표시합니다.
- 북아시아 언어 등에서 분해, 조합, 재정렬을 수행하는 언어의 글을 표시합니다.
- 세계의 여러 비슷해 보이는 문자들 간 발생할 수 있는 보안 문제를 고려합니다.

#### Characters and Glyphs
**문자와 모양**

유니코드는 문자가 해석되는 방식만을 정의할 뿐 문자의 모양이 어떻게 표시되는지는
정의하지 않습니다.

#### Text Elements
**글의 원소**

코드 포인트는 0-10FFFF(16진수) 사이의 숫자입니다. 글은 하나 이상의 코드 포인트로
구성됩니다.


2\. General Structure
---------------------
**일반적 구조**

### 2.1 Architectural Context
**설계적 맥락**

유니코드 표준은 문자 코드를 이용해 여러가지 유용한 처리를 제공합니다.

#### Basic Text Processes
**기본 글자 처리**

대부분의 컴퓨터는 적은 수의 다음과 같은 기본적 글자 처리를 제공합니다.
- 글자의 시각적 표시
- 줄 넘기기
- 글자 크기, 굵기 등의 변형
- 단어와 문장의 판별
- 글자 선택이나 강조
- 키보드 입력, 삽입, 삭제
- 검색이나 정렬을 위한 비교
- 철자 검사, 하이픈, 형태론 분석
- 압축, 압축 해제, 자르기, 송/수신

#### Text Elements, Characters, and Text Processes
**글의 원소, 문자와 글 처리**

글의 원소는 언어나 맥락에 따라 달라집니다. 예를 들면 같은 라틴 문자 알파벳 두 개라도
언어에 따라 한 글자로 인식되기도 하며, 영어의 대문자와 소문자는 다른 글자라도
검색시에는 같은 글자로 인식되어야 합니다.
또한 단어 단위 처리에서는 한 글의 원소가 한 개 이상의 문자로 구성되기도 합니다.

최소한의 문자 단위는 _할당된 문자_ 라고 부릅니다.

사용자가 인식하기에 하나의 문자로 판단되는 것을 _그래핌 클러스터_ 라고 합니다.

#### Text Processes and Encoding
**글 처리와 인코딩**

여러 언어에서는, 영어와 달리 왼쪽에서 오른쪽으로, 선형적으로 글자가 표시되지만은
않습니다. 구체적인 예시는 [Arabic](#92-arabic), [Devanagari](#121-devanagari)
항목을 참고하세요.

억양이 추가된 불어, 스웨덴어에서 사용되는 인코딩은 두 가지가 있습니다.
“ä”, “ö” 등을 한개의 문자로 처리하거나, 두 개의 조합된 문자로 취급하는 방식이
있습니다.

인코딩은 모든 글을 동등하게 잘 처리하지 못합니다. 구현에는 각각의 장단점이 있습니다.

문자열 비교 알고리즘은 단순히 순차적으로 처리할 수 없습니다. 표준적인 기본 문자열
비교 메커니즘에 대한 상세한 내용은
[Unicode Technical Standard #10, “Unicode Collation Algorithm,”]() 에서
확인하세요.

_Comment: 추가 내용 요약_

### 2.2 Unicode Design Principles

#### Universality

#### Efficiency

#### Characters, Not Glyphs

#### Semantics

#### Plain Text

#### Logical Order

#### Unification

#### Dynamic Composition

#### Stability

#### Convertibility

### 2.3 Compatibility Characters

#### Compatibility Variants

#### Compatibility Decomposable Characters

### 2.4 Code Points and Characters

#### Types of Code Points

### 2.5 Encoding Forms

#### UTF-32

#### UTF-16

#### UTF-8

#### Comparison of the Advantages of UTF-32, UTF-16, and UTF-8

### 2.6 Encoding Schemes

### 2.7 Unicode Strings

### 2.8 Unicode Allocation

#### Planes

#### Allocation Areas and Blocks

#### Assignment of Code Points

### 2.9 Details of Allocation

#### Plane 0 (BMP)

#### Plane 1 (SMP)

#### Plane 2 (SIP)

#### Other Planes

### 2.10 Writing Direction

### 2.11 Combining Characters

#### Sequence of Base Characters and Diacritics

#### Multiple Combining Characters

#### Ligated Multiple Base Characters

#### Exhibiting Nonspacing Marks in Isolation

#### “Characters” and Grapheme Clusters

### 2.12 Equivalent Sequences

#### Normalization

#### Decompositions

#### Non-decomposition of Certain Diacritics

### 2.13 Special Characters

#### Special Noncharacter Code Points

#### Byte Order Mark (BOM)

#### Layout and Format Control Characters

#### The Replacement Character

#### Control Codes

### 2.14 Conforming to the Unicode Standard
#### Characteristics of Conformant Implementations

#### Unacceptable Behavior

#### Acceptable Behavior

#### Supported Subsets
