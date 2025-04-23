1). Снимаю все ифаки
и прибиваю неиспользуемые модели

Staff - int+b2b

int only:

City 
Office
Department
DepartmentStaff
DepartmentStaffCounter
StaffInflection
Service
ServiceRole
ServiceMember
Group
GroupMembership
Country

+ DepartmentKind

2) 


INTRANET_MODELS_STAFF = (
    'birthday',
    'gender',
    'family',       # family_status, children
    'car',          # car, car_num
    'address',
    'education',    # edu_status, edu_date, edu_place
    'department',   # department (key to Department)
    'is_dismissed',
    'office',
    'desk_id',
    'wiki_name',
    'join_at',
    'quit_at',
    'position',
    'employment',
    'contacts',     # equals 'work_phone' + 'mobile_phone' + 'work_email'
    'work_phone',
    'mobile_phone',
    'work_email',
    'vacation',
    'lang',
    'service_profile',
    'uid',
)