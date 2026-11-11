# Description

Tadabbr is a website that helps users search poetry extracted from arabic quranic tafasirs.

# Data sources

Data is scraped from websites like islamweb or shamla then saved to a migration postgresql file.
the data scraping is not the work of the backend, rather a seperate proccess which will probably be in python. https://github.com/Tadabbr/Tadabbr-Scraper

# requirements
the web platform should support the next features.
- search by poetry
- search by ayah
- search by poet
- search by mufassir
- user reports of data issues

# database
export DATABASE_URL="postgresql://postgres:password@localhost:5432/postgres?sslmode=disable"
tables:

users:
```sql
	id UUID PRIMARY KEY DEFAULT gen_random_-uuid(),
    clerk_user_id TEXT UNIQUE NOT NULL,
    created_at TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP
	updated_at TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP
```

user_profiles:
```sql
   id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
   user_id UUID NOT NULL UNIQUE REFERENCES users ON DELETE CASCADE,
   avatar_url TEXT,
   bio TEXT ,
   created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
   updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP 
```

user_reports
```sql
id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
poem_id UUID REFERENCES poems ON DELETE CASCADE
reporter_id UUID REFERENCES users ON DELETE SET NULL 
report text NOT NULL
created_at TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP
```
ayat:
```sql
global_ayah_number smallint PRIMARY KEY  -- ayah number in the quran as a whole.
ayah text NOT NULL 
verse_key text NOT NULL -- verse_key surahN:ayahN
created_at TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP
```

poets:
```sql
id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
name text NOT NULL
aldiwan_url text UNIQUE -- link to the poet's aldiwan page
created_at TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP
```

poems:
```sql
id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
poem text  NOT NULL
poet_id text  REFERERNCES poets(id) ON DELETE RESTRICT 
created_at TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP
```

tafsir_poems:
```sql
CREATE TABLE tafsir_poems (
    tafsir_id UUID NOT NULL
        REFERENCES tafasirs(id)
        ON DELETE CASCADE,

    poem_id UUID NOT NULL
        REFERENCES poems(id)
        ON DELETE CASCADE,

    context_before TEXT,
    context_after TEXT,

    PRIMARY KEY (tafsir_id, poem_id)
);
```

Tafasir:
```sql
id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
name TEXT NOT NULL,
tafsir_url TEXT UNIQUE NOT NULL
created_at TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP
```
muffassiron:
```sql
id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
name text NOT NULL
biography_url TEXT -- a trusted source for the biography of the mufassir
```

mufassiron_tafsir:
```sql
CREATE TABLE tafsir_mufassirs (
    tafsir_id UUID NOT NULL REFERENCES tafasirs(id) ON DELETE CASCADE,
    mufassir_id UUID NOT NULL REFERENCES mufassirs(id) ON DELETE CASCADE,
    PRIMARY KEY (tafsir_id, mufassir_id)
```



# Api

## User Action map
```
VISITOR
│
├── Search
│   ├── poetry
│   ├── ayah
│   ├── poet
│   ├── mufassir
│   └── tafsir
│
├── Explore
│   ├── view poem
│   ├── view ayah
│   ├── view poet
│   ├── view mufassir
│   └── view tafsir
│
└── Authentication
    ├── sign up
    ├── login
    └── logout


AUTHENTICATED USER
│
├── Everything above
│
├── Profile
│   ├── view profile
│   ├── update profile
│   └── delete account
│
├── Reports
│   ├── create report
│   ├── view my reports
│   └── view report status
│
└── Personalization
    ├── bookmark poem
    ├── remove bookmark
    └── view bookmarks


ADMIN
│
├── Reports
│   ├── list reports
│   ├── inspect report
│   ├── resolve report
│   └── reject report
│
└── Data moderation
    ├── correct data
    ├── disable bad data
    └── etc.

```

## Essential actions
```
1. Search
2. View poem
3. View ayah
4. View poet
5. View mufassir
6. View tafsir
7. Create report
8. View own profile
9. Update own profile
```

## endpoints
