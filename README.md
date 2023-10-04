## Introduction

This is a small project in its initial stages that is intended to be a small 
streaming platform that people can listen to music, or upload their own.
Below is a screenshot of the project in its current state:

![image](https://github.com/conorbowles51/StreamingPlatform/assets/143211735/a54760d0-3df1-4c3e-9b1d-4f617260d8de)


## About the project

The project uses Next.js, Tailwind for styling, and custom components made with React.
It is intended to be a fully responsive app and should adapt to whatever screen size
it is run on. I have included below a screenshot of how the app reacts to a mobile viewport.

![image](https://github.com/conorbowles51/StreamingPlatform/assets/143211735/ba66d264-c53d-444e-8f69-328132de0e95)

It is currently styled to have a similar aesthetic to Spotify.

## A look into some of the components I've created

# Sidebar component
```
interface SidebarProps {
    children: React.ReactNode;
}

const Sidebar: React.FC<SidebarProps> = ({
    children
}) => {
    const pathname = usePathname();

    const routes = useMemo(() => [
        {
            icon: HiHome,
            label: 'Home',
            active: pathname !== '/search',
            href: '/'
        },

        {
            icon: BiSearch,
            label: 'Search',
            active: pathname === '/search',
            href: '/search'
        }
    ], [pathname])

    return ( 
        <div className="flex h-full">
            <div className="hidden md:flex flex-col gap-y-2 bg-black h-full w-[300px] p-2">
                <Box>
                    <div className="flex flex-col gap-y-4 px-5 py-4">
                        {routes.map((item) => (
                            <SidebarItem 
                                key={item.label}
                                {...item}
                            />
                        ))}
                    </div>
                </Box>
                <Box className="overflow-y-auto h-full">
                    <Library />
                </Box>
            </div>
            <main className="h-full flex-1 overflow-y-auto py-2">
                {children}
            </main>
        </div>
     );
}
 
export default Sidebar;
```
The above code is what generates the sidebar component, which will only be visible on medium
and above sized screens (i.e tablet or computer monitor). The 'usePathname' hook gives me access to the
current URL's path name. The navigational routes for this component are stored as objects with the 
'useMemo' hook so that the 'active' property of the object gets updated correctly depending on the 
pathname, which is listed in the dependancy array of the useMemo hook. These routes are then mapped over
and displayed as <SidebarItem> elements. Although there are only two routes right now, the 'Home' and 'Search'
route, this method of implementation makes it much easier for me to add more routes down the line if I need to.

## Next steps

The next steps for this project is to hook up the database tables that I have created with Supabase
and allow for users to upload and listen to music. I will also be implenting an authentification system,
probably using Clerk.js, and payment methods using Stripe.

## Running the project

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000] with your browser to see the result.
